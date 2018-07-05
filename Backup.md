## Backup script for MongoDB Data, if running Snap MongoDB at port 27019

```sh
#!/bin/bash
now=$(date +'%Y-%m-%d_%H.%M.%S')
mkdir -p backups/$now
cd backups/$now
mongodump --port 27019
# if running on source install, run for example: mongodump --port 27017)
cd ..
zip -r $now.zip $now
cd ../..
echo "\nBACKUP DONE."
echo "Backup is at directory backups/${now}."
echo "Backup is also archived to .zip file backups/${now}.zip"
```

## Docker Backup and Restore

[Docker Backup and Restore](https://github.com/wekan/wekan/wiki/Export-Docker-Mongo-Data)

[Wekan Docker Upgrade](https://github.com/wekan/wekan-mongodb#backup-before-upgrading)

## Snap Backup

[Snap Backup and Restore](https://github.com/wekan/wekan-snap/wiki/Backup-and-restore)

[Wekan Snap upgrade](https://github.com/wekan/wekan-snap/wiki/Install#5-install-all-snap-updates-automatically-between-0200am-and-0400am)

## Sandstorm Backup

Download Wekan grain with arrow down download button to .zip file. You can restore it later.

[Export data from Wekan Sandstorm grain .zip file](https://github.com/wekan/wekan/wiki/Export-from-Wekan-Sandstorm-grain-.zip-file)

## Python Backup Script for Wekan Docker environment
```py
#!/usr/bin/env python3

import os
import sys
import subprocess
import configparser
import time
import datetime
import smtplib
import traceback
import logging
import gzip
import yaml
import abc
import shutil


class Config:
  __conf = {
    "db_name" : '',
    "retention" : '',
    "dump_path" : '',
    "container" : '',
    "start_date" : time.strftime('%Y%m%d-%H%M%S'),
    "curdate" : time.strftime('%Y-%m-%d %X')
  }

  __setters = ["db_name", "retention", "dump_path", "container"]

  @staticmethod
  def config(name):
    return Config.__conf[name]

  @staticmethod
  def set(name, value):
    if name in Config.__setters:
      Config.__conf[name] = value
    else:
      raise NameError("Name not accepted in set() method")


class Dbms(metaclass=abc.ABCMeta):
  def __init__(self, db_name, container, dump_path):
    self._database = db_name
    self._dumpfile = os.path.join(dump_path, self.getdumpfilename())
    self._container = container
    self._compression = CompressionGzip()
    self._dump_path = dump_path

  @abc.abstractmethod
  def dump(self):
    pass

  def getdumpfilename(self):
    return 'dump-{}-{}'.format(self._database, Config.config('start_date'))

class DbmsMongodb(Dbms):
  def dump(self):
    call = 'docker exec {} bash -c "mongodump -d {} -o /dump/"'.format(self._container, self._database)
    try:
      output = subprocess.check_output(call, universal_newlines=True, shell=True)
    except subprocess.CalledProcessError as e:
      raise Exception('Mongodump failed due to the following Error: {}'.format(e))
    call = 'docker cp {}:/dump {}'.format(self._container, self._dump_path)
    try:
      output = subprocess.check_output(call, universal_newlines=True, shell=True)
    except subprocess.CalledProcessError as e:
      raise Exception('Pulling dump from container failed due to the following Error: {}'.format(e))
    call = 'tar -C {}/dump -cf {} .'.format(self._dump_path, self._dumpfile + '.tar')
    try:
      output = subprocess.check_output(call, universal_newlines=True, shell=True)
    except subprocess.CalledProcessError as e:
      raise Exception('Creating .tar-ball failed due to the following Error: {}'.format(e))
    self._compression.setFilename(self._dumpfile + '.tar')
    self._compression.compress()
    shutil.rmtree(self._dump_path + '/dump')


class Compression(metaclass=abc.ABCMeta):
  def __init__(self):
    self._filename = ''

  def setFilename(self, filename):
    self._filename = filename

  @abc.abstractmethod
  def compress(self):
    pass


class CompressionGzip(Compression):
  def compress(self):
    call = 'gzip {}'.format(self._filename)
    try:
      output = subprocess.check_output(call, universal_newlines=True, shell=True)
    except subprocess.CalledProcessError as e:
      raise Exception('Compression failed due to the following Error: {}'.format(e))
    else:
      #print('Successfully created dump: {}'.format(self._filename + '.gz'))
      pass

#DB-Config-File-Checker: checks if the file passed in the function call is accessible, if not, raise exception
def checkcfg(conf):
  if(os.path.isfile(conf)):
    config_file = conf
  else:
    raise Exception("Specified Config File doesn't exist or insufficient access rights")
  checkpermission(config_file)
  return config_file

def checkpath(path):
  if not os.path.exists(path):
    os.makedirs(path)

def checkpermission(cfg):
  if (os.stat(cfg).st_uid != 0):
    raise Exception("Config file must be owned by user root!")
  elif (os.stat(cfg).st_gid != 0):
    raise Exception("Config file must be owned by group root!")
  else:
    accessmask = oct(os.stat(cfg).st_mode)[-3:]
    if accessmask == '600' or accessmask == '700':
      pass
    else:
      raise Exception("Root must have read and write access to config file, all other users mustn't be allowed. Current Access Mask: {} but it should be 600 or 700".format(accessmask))
    pass



def parseInput():
  sys.tracebacklimit = None
  #check if the script has been called with one argument --> The db-specific config file
  if len(sys.argv) != 2:
    raise Exception("usage: wekandump.py <path_to_configfile> \n Please specify the path to a configfile")

  #Send the specified db-config file to the Configuration-Checker
  config_file = checkcfg(sys.argv[1])

  #Now that both of the config-files have been checked, finally open them
  with open(sys.argv[1], 'r') as cfgfile:
    cfg = yaml.safe_load(cfgfile)


  #Set some vars using data from the config-file
  Config.set('db_name', cfg['dumps']['database'])
  Config.set('retention', cfg['dumps']['retention'])
  Config.set('dump_path', cfg['dumps']['path'])
  Config.set('container', cfg['dumps']['container'])

  checkpath(Config.config('dump_path'))

  cfgfile.close

def dumpcompress():
    dbms = DbmsMongodb(Config.config('db_name'), Config.config('container'), Config.config('dump_path'))
    dbms.dump()


def getcrtime(item):
  call = 'stat -c %y {}'.format(item)
  output = subprocess.check_output(call, universal_newlines=True, shell=True)
  output = output.rstrip()
  crtime = datetime.datetime.fromtimestamp(os.stat(item).st_mtime)
  return crtime

def housekeep():
  #get all filenames located in the dump-directory
  call = 'ls {}'.format(Config.config('dump_path'))
  output = subprocess.check_output(call, universal_newlines=True, shell=True)
  output = output.rstrip()
  dumps = output.split('\n')
  #now that we have a list with the filenames of the files in the dump-folder, every filename is handled seperately
  for item in dumps:
    item = os.path.join(Config.config('dump_path'), item)
    crtime = getcrtime(item)
    curtime = datetime.datetime.strptime(Config.config('curdate'), '%Y-%m-%d %X')
    if (curtime-crtime).days >= Config.config('retention'):
      try:
        os.remove(item)
      except:
        try:
          shutil.rmtree(item)
        except:
          raise Exception('Housekeep: failed to delete the dump {}'.format(item))
        else:
          #print("Housekeep: Deleted dump: {}, it has reached the age of {} days. (Retention is {} days.)".format(item, curtime-crtime, Config.config('retention')))
          pass
      else:
        #print("Housekeep: Deleted dump: {}, it has reached the age of {} days. (Retention is {} days.)".format(item, curtime-crtime, Config.config('retention')))
        pass
    else:
      #print("Housekeep: Dump {} was kept since it is only {} hours old. (Retention is {} days.)".format(item, curtime-crtime, Config.config('retention')))
      pass


def main():
  parseInput()
  dumpcompress()
  housekeep()

if __name__ == "__main__":
  main()
```