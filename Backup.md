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