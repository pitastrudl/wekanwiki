## Related talk about MongoDB backup

Related talk, search for "mongodb" this page:
https://fosdem.org/2020/schedule/events/

There is this:

Percona Backup for MongoDB: Status and Plans

Open Source solution for consistent backups of multi-shard MongoDB

- [Slides](https://fosdem.org/2020/schedule/event/perconamongodb/attachments/slides/3768/export/events/attachments/perconamongodb/slides/3768/Percona_Backup_for_MongoDB.pdf)
- [Video webm](https://video.fosdem.org/2020/UD2.119/perconamongodb.webm)
- [Same Video mp4](https://video.fosdem.org/2020/UD2.119/perconamongodb.mp4)

## Related Sandstorm issue

[Creating a backup while the grain is running could cause corruption](https://github.com/sandstorm-io/sandstorm/issues/3186).

## Combining old and new Wekan version data

Note: Do mongodump/mongorestore only when Wekan is stopped: wekan.wekan (Snap) or wekan-app (Docker).

1. From new Wekan export all boards to Wekan JSON.
2. Backup new Wekan with mongodump.
3. Backup old Wekan with mongodump.
4. Restore old Wekan data to new Wekan with mongorestore.
5. Restore new Wekan JSON exported boards by importing them.

## Rescuing board that does not load

Wekan web UI Import/Export JSON does not have all content currently. To upgrade from old Wekan version, use mongodump/mongorestore to newest Wekan, like described below.

To import big JSON file, on Linux you can use xclip to copy textfile to clipboard:
```
sudo apt-get install xclip
cat board.json | xclip -se c
```
Then paste to webbrowser Wekan Add Board / Import / From previous export.

You can [save all MongoDB database content as JSON files](https://github.com/wekan/wekan/wiki/Export-from-Wekan-Sandstorm-grain-.zip-file). Files are base64 encoded in JSON files.

Export board to Wekan JSON, and import as Wekan JSON can make some part of board to load, but you should check is some data missing.

With Wekan Snap, you can use [nosqlbooster GUI](https://nosqlbooster.com/downloads) to login through SSH to Wekan server localhost port 27019 and browse data.

You could use [daff](https://github.com/paulfitz/daff) to compare tables.

## [Cloud Backup with rclone](https://github.com/wekan/wekan/wiki/Backup#cloud-backup-with-rclone)

## Using Snap Mongo commands on your bash CLI

Add to your `~/.bashrc`
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/snap/wekan/current/lib/x86_64-linux-gnu
export PATH="$PATH:/snap/wekan/current/bin"
```
Then you can backup:
```
mongodump --port 27019
```
And restore:
```
mongorestore --drop --port 27019
```

## MongoDB shell on Wekan Snap

mongoshell.sh
```bash
#/bin/bash
version=$(snap list | grep wekan | awk -F ' ' '{print $3}')
mongo=$"/snap/wekan/$version/bin/mongo"
$mongo --port 27019
```

***

# Snap backup-restore v2

Originally from https://github.com/wekan/wekan-snap/issues/62#issuecomment-470622601

## Backup

wekan-backup.sh
```
#!/bin/bash
export LC_ALL=C
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/snap/wekan/current/lib/x86_64-linux-gnu

version=$(snap list | grep wekan | awk -F ' ' '{print $3}')
now=$(date +"%Y%m%d-%H%M%S")
parent_dir="/data/backups/wekan"
backup_dir="${parent_dir}/${now}"
log_file="${parent_dir}/backup-progress.log.${now}"

error () {
  printf "%s: %s\n" "$(basename "${BASH_SOURCE}")" "${1}" >&2
  exit 1
}

trap 'error "An unexpected error occurred."' ERR

take_backup () {
  mkdir -p "${backup_dir}"

  cd "${backup_dir}"

  /snap/wekan/$version/bin/mongodump --quiet --port 27019

  cd ..

  tar -zcf "${now}.tar.gz" "${now}"

  rm -rf "${now}"
}

printf "\n======================================================================="
printf "\nWekan Backup"
printf "\n======================================================================="
printf "\nBackup in progress..."

take_backup 2> "${log_file}"

if [[ -s "${log_file}" ]]
then
  printf "\nBackup failure! Check ${log_file} for more information."
  printf "\n=======================================================================\n\n"
else
  rm "${log_file}"
  printf "...SUCCESS!\n"
  printf "Backup created at ${backup_dir}.tar.gz"
  printf "\n=======================================================================\n\n"
fi
```
wekan-restore.sh
```
#!/bin/bash
export LC_ALL=C
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/snap/wekan/current/lib/x86_64-linux-gnu

makesRestore()
{
    file=$1

    ext=$"$(basename $file)"
    parentDir=$"${file:0:${#file}-${#ext}}"
    cd "${parentDir}"

    printf "\nMakes the untar of the archive.\n"

    tar -zxvf "${file}"
    file="${file:0:${#file}-7}"

    version=$(snap list | grep wekan | awk -F ' ' '{print $3}')

    restore=$"/snap/wekan/${version}/bin/mongorestore"

    printf "\nThe database restore is in progress.\n\n"

    ## Only if you get errors about existing indexes, use this below instead:
    ## $restore --quiet --drop --noIndexRestore -d wekan --port 27019 "${file}/dump/wekan"

    $restore --quiet --drop -d wekan --port 27019 "${file}/dump/wekan"

    rm -rf "${file}"

    printf "\nRestore done.\n"
}

makesRestore $1
```

***

# Snap backup-restore v1

## Backup script for MongoDB Data, if running Snap MongoDB at port 27019

```sh
#!/bin/bash

makeDump()
{
    # Gets the version of the snap.
    version=$(snap list | grep wekan | awk -F ' ' '{print $3}')

    # Prepares.
    now=$(date +'%Y-%m-%d_%H.%M.%S')
    mkdir -p /var/backups/wekan/$version-$now

    # Targets the dump file.
    dump=$"/snap/wekan/$version/bin/mongodump"

    # Makes the backup.
    cd /var/backups/wekan/$version-$now
    printf "\nThe database backup is in progress.\n\n"
    $dump --port 27019

    # Makes the tar.gz file.
    cd ..
    printf "\nMakes the tar.gz file.\n"
    tar -zcvf $version-$now.tar.gz $version-$now

    # Cleanups
    rm -rf $version-$now

    # End.
    printf "\nBackup done.\n"
    echo "Backup is archived to .tar.gz file at /var/backups/wekan/${version}-${now}.tar.gz"
}

# Checks is the user is sudo/root
if [ "$UID" -ne "0" ]
then
    echo "This program must be launched with sudo/root."
    exit 1
fi


# Starts
makeDump

```

## Restore script for MongoDB Data, if running Snap MongoDB at port 27019 with a tar.gz archive.

```sh
#!/bin/bash

makesRestore()
{
    # Prepares the folder used for the backup.
    file=$1
    if [[ "$file" != *tar.gz* ]]
    then
        echo "The backup archive must be a tar.gz."
        exit -1
    fi

    # Goes into the parent directory.
    ext=$"$(basename $file)"
    parentDir=$"${file:0:${#file}-${#ext}}"
    cd $parentDir

    # Untar the archive.
    printf "\nMakes the untar of the archive.\n"
    tar -zxvf $file
    file="${file:0:${#file}-7}"
    
    # Gets the version of the snap.
    version=$(snap list | grep wekan | awk -F ' ' '{print $3}')

    # Targets the dump file.
    restore=$"/snap/wekan/$version/bin/mongorestore"

    # Restores.
    printf "\nThe database restore is in progress.\n\n"
    ## Only if you get errors about existing indexes, use this below instead:
    ## $restore --drop --noIndexRestore wekan --port 27019 $file/dump/wekan
    $restore --drop wekan --port 27019 $file/dump/wekan
    printf "\nRestore done.\n"

    # Cleanups
    rm -rf $file
}

# Checks is the user is sudo/root.
if [ "$UID" -ne "0" ]
then
    echo "This program must be launched with sudo/root."
    exit 1
fi


# Start.
makesRestore $1

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

# Cloud Backup with [rclone](https://rclone.org)
This does backup of [Wekan+RocketChat snap databases](https://github.com/wekan/wekan/wiki/OAuth2) and php website etc.

```
sudo su
export EDITOR=nano
crontab -e
```
Backup every 15 minutes. Also set Wekan mail url manually once a day because of [bug](https://github.com/wekan/wekan-snap/issues/78).
```
# m h  dom mon dow   command
15 * * * * /root/backup.sh >> /root/backup.log.txt 2>&1
15 17 * * * snap set wekan mail-url='smtps://boards%40example.com:user@mail.example.com.com:465/'
15 17 * * * snap set wekan mail-from='Wekan Boards Support <boards@example.com>'
```
/root/backup.sh, that is set executeable: chmod +x backup.sh

Uses [rclone](https://rclone.org).
```
cd /root
./backup-wekan.sh
./backup-rocketchat.sh
./backup-website.sh
rclone move backups cloudname:backup.example.com
```
/root/rclone-ls-all.sh , shows directory contests at cloud:
```
rclone lsd cloudname:
```
/root/backup-wekan.sh
```
#!/bin/bash

makeDump()
{

    backupdir="/root/backups/wekan"

    # Gets the version of the snap.
    version=$(snap list | grep wekan | awk -F ' ' '{print $3}')

    # Prepares.
    now=$(date +'%Y-%m-%d_%H.%M.%S')
    mkdir -p $backupdir/$version-$now

    # Targets the dump file.
    #dump=$"/snap/wekan/$version/bin/mongodump"

    # Makes the backup.
    cd $backupdir/$version-$now
    printf "\nThe database backup is in progress.\n\n"
    mongodump --port 27019

    # Makes the tar.gz file.
    cd ..
    printf "\nMakes the tar.gz file.\n"
    tar -zcvf $version-$now.tar.gz $version-$now

    # Cleanups
    rm -rf $version-$now

    # End.
    printf "\nBackup done.\n"
    echo "Backup is archived to .tar.gz file at $backupdir/${version}-${now}.tar.gz"
}

# Checks is the user is sudo/root
if [ "$UID" -ne "0" ]
then
    echo "This program must be launched with sudo/root."
    exit 1
fi

# Starts
makeDump
```
/root/backup-rocketchat.sh
```
#!/bin/bash

makeDump()
{

    backupdir="/root/backups/rocketchat"

    # Gets the version of the snap.
    version=$(snap list | grep wekan | awk -F ' ' '{print $3}')

    # Prepares.
    now=$(date +'%Y-%m-%d_%H.%M.%S')
    mkdir -p $backupdir/$version-$now

    # Targets the dump file.
    dump=$"/snap/wekan/$version/bin/mongodump"

    # Makes the backup.
    cd $backupdir/$version-$now
    printf "\nThe database backup is in progress.\n\n"
    $dump --port 27017

    # Makes the tar.gz file.
    cd ..
    printf "\nMakes the tar.gz file.\n"
    tar -zcvf $version-$now.tar.gz $version-$now

    # Cleanups
    rm -rf $version-$now

    # End.
    printf "\nBackup done.\n"
    echo "Backup is archived to .tar.gz file at $backupdir/${version}-${now}.tar.gz"
}

# Checks is the user is sudo/root
if [ "$UID" -ne "0" ]
then
    echo "This program must be launched with sudo/root."
    exit 1
fi

# Starts
makeDump
```
/root/backup-website.sh
```
#!/bin/bash

makeDump()
{

    backupdir="/root/backups/example.com"

    # Gets the version of the snap.
    version=$(snap list | grep wekan | awk -F ' ' '{print $3}')

    # Prepares.
    now=$(date +'%Y-%m-%d_%H.%M.%S')
    mkdir -p $backupdir/$version-$now

    # Makes the backup.
    cd $backupdir/$version-$now
    printf "\nThe file backup is in progress.\n\n"

    # Makes the tar.gz file.
    cd ..
    printf "\nMakes the tar.gz file.\n"
    cp -pR /var/snap/wekan/common/example.com $version-$now
    tar -zcvf $version-$now.tar.gz $version-$now

    # Cleanups
    rm -rf $version-$now

    # End.
    printf "\nBackup done.\n"
    echo "Backup is archived to .tar.gz file at $backupdir/${version}-${now}.tar.gz"
}

# Checks is the user is sudo/root
if [ "$UID" -ne "0" ]
then
    echo "This program must be launched with sudo/root."
    exit 1
fi

# Starts
makeDump
```
/var/snap/wekan/common/Caddyfile
```
chat.example.com {
	proxy / localhost:3000 {
	  websocket
	  transparent
	}
}

https://boards.example.com {
	proxy / localhost:3001 {
	  websocket
	  transparent
	}
}

example.com {
	root /var/snap/wekan/common/example.com
	fastcgi / /var/run/php/php7.0-fpm.sock php
}

matomo.example.com {
        root /var/snap/wekan/common/matomo.example.com
        fastcgi / /var/run/php/php7.0-fpm.sock php
}

# Example CloudFlare free wildcard SSL Origin Certificate, there is example.com.pem at certificates directory with private key at to and cert at bottom.
http://example.com https://example.com {
        tls {
            load /var/snap/wekan/common/certificates
            alpn http/1.1
        }
        root /var/snap/wekan/common/example.com
        browse
}

static.example.com {
	root /var/snap/wekan/common/static.example.com
}
```