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
    $restore -d wekan --port 27019 $file/dump/wekan
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

## Python Backup Script for Wekan Docker environment

[Use Python to backup your Mongo Data, with automatic cleanup](https://github.com/wekan/wekan/wiki/Python-Backup-Script-for-Wekan-Docker-environment)