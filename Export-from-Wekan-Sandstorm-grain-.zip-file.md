This is useful for example if you get [Board not found error](https://github.com/wekan/wekan/issues/1430)

## 1) Download Wekan grain

Use Sandstorm arrow down button to download Wekan grain in .zip file.

## 2) Unzip downloaded file

## 3) Install latest Wekan, or only MongoDB 3.2.20 or newer locally

[Install from releases page](https://github.com/wekan/wekan/releases)

## 4) Stop Wekan and MongoDB

## 5) Copy database files from unzipped Wekan grain to MongoDB

In .zip file database files are in directory `data/wiredTigerDb/`

In Wekan Snap, database files are in directory `/var/snap/wekan/common` - if you have other data there, rename common directory to other name first. 

[Snap Backup and Restore](https://github.com/wekan/wekan-snap/wiki/Backup-and-restore)

[Docker Backup and Restore](https://github.com/wekan/wekan/wiki/Export-Docker-Mongo-Data)

## 6) Change database file permissions to root user

In Snap:
```
sudo chown root:root /var/snap/wekan/common -R
```

## 7) Start MongoDB

In Snap:
```
sudo snap start wekan.mongodb
```

## 8) Or, if you are brave, also start standalone wekan

Try does Standalone Wekan work with that database
```
sudo snap start wekan.mongodb
sudo snap start wekan.wekan
```
or both wekan and database at once
```
sudo snap start wekan
```

## 9) To see MongoDB data, install Robo3T GUI

https://robomongo.org

Wekan Snap: Connect it to address `localhost:27019`

Wekan Docker: If you have MongoDB exposed to outside Docker, Connect with Robo3T to address `localhost:27017`. Otherwise you first need to copy files from wekan-db Docker container to outside of Docker container, and restore files to local separately installed MongoDB database v3.2.20 or newer

[Snap Backup and Restore](https://github.com/wekan/wekan-snap/wiki/Backup-and-restore)

[Docker Backup and Restore](https://github.com/wekan/wekan/wiki/Export-Docker-Mongo-Data)

## 10) Browse data in Robo 3T

- On left, double click cards, checklists etc collections/tables to see their contents
- Currently default view to see is tree view. To see table view or JSON view, click small buttons above that white data area view display at near right border.

## 11) If you don't find data in Robo 3T, use hex editor GUI

In Linux, you can install Hex Editor for example with command:
```
sudo apt install ghex
```
or
```
sudo yum install ghex
```
Then it's usually in Linux desktop at Menu / Development / GHex.
Or you can start it in command line by writing `ghex`

You can open files from your unzipped Wekan Sandstorm grain directory `data/wiredTigerDb/` to see if there is still some data that is not yet overwritten with other data.

## 12) Moving data from Sandstorm to Standalone Wekan like Snap or Docker

12.1 Compare databases of Sandstorm and Docker Wekan with mongo GUI https://nosqlbooster.com/

12.2 Create new user to Standalone Wekan

12.3 Copy new user bcrypt password structure created bcrypt encrypted password from Sandstorm to Docker wekan structure. It's at users collection/table.

12.4 Login

12.5 Here is info about script how to save all from MongoDB to .JSON textfiles https://forums.rocket.chat/t/big-issue-with-custom-javascript/261/4
and most likely how to get them back to mongodb
so just copying all of those boards JSON files and restoring to MongoDB database would work
and editing JSON files with any plain text editor. For big files you can try JEdit.

12.6 Here is how to backup and restore mongodb in docker, snap etc https://github.com/wekan/wekan/wiki/Backup

12.7 All Wekan Docker settings are in this textfile https://raw.githubusercontent.com/wekan/wekan/devel/docker-compose-build.yml