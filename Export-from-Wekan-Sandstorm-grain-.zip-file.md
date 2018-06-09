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
