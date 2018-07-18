## Backup script for MongoDB Data, if running Snap MongoDB at port 27019

```sh
#!/bin/bash

makeDump()
{
    # Gets the version of the snap.
    version=$(snap list | grep wekan | awk -F ' ' '{print $3}')

    # Prepares.
    now=$(date +'%Y-%m-%d_%H.%M.%S')
    mkdir -p /var/backups/wekan/$now

    # Targets the dump file.
    dump=$"/snap/wekan/$version/bin/mongodump"

    # Makes the backup.
    cd /var/backups/wekan/$now
    printf "\nThe backup of the database is starting.\n\n"
    $dump --port 27019

    # Makes the zip file.
    cd ..
    printf "\nMakes the zip.\n"
    zip -r $now.zip $now

    # Cleanups
    rm -rf $now

    # End.
    printf "\nBackup done.\n"
    echo "Backup is archived to .zip file at /var/backups/wekan/${now}.zip"
}

# Checks is the user is sudo/root
if [ "$UID" -ne "0" ]
then
    echo "This program must be launched with sudo/root."
    exit 1
fi


# Start
makeDump

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

[Use Python to backup your Mongo Data, with automatic cleanup](https://github.com/wekan/wekan/wiki/Python-Backup-Script-for-Wekan-Docker-environment)