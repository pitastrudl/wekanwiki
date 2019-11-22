## Why test

https://github.com/wekan/wekan/issues/2811

## Who should test
- If you are the person in your company that gets yelled at when something breaks in new version of Wekan
- If you think xet7 releasing new version of Wekan every day directly to stable production channel is in any way risky

## Testers to ping with new release
- All those whose issues were fixed
- @saschafoerster 

## ChangeLog

https://github.com/wekan/wekan/blob/master/CHANGELOG.md

## Backup before testing. And backup daily in production.

Why? Well, Wekan has no undo yet. If you delete Swimlane/List/Card, it's gone.
That's why it's harder to reach in submenu. It's better to Arhive those,
and unarchive.

https://github.com/wekan/wekan/wiki/Backup

You could test at other computer than your production.

## Snap

Snap has automatic update, or you can update manually:
```
sudo snap refresh
```
You see at https://snapcraft.io/wekan what are current versions.

To change to Edge:
```
sudo snap refresh wekan --edge --amend
```
And back to stable:
```
sudo snap refresh wekan --stable --amend
```

## Docker

docker-compose.yml is at https://github.com/wekan/wekan .

### Latest development version from master branch

Quay:
``
image: quay.io/wekan/wekan
```
Docker Hub:
```
image: wekanteam/wekan
```

### Example of using release tags

Quay:
``
image: quay.io/wekan/wekan:v3.55
```
Docker Hub:
```
image: wekanteam/wekan:v3.55
```

## How to change Docker version

1) Backup first
https://github.com/wekan/wekan/wiki/Backup

```
docker-compose stop
docker rm wekan-app
```
2) Change version tag. Then:
```
docker-compose up -d
```

## Sandstorm

1) Install local development version of Sandstorm to your laptop from https://sandstorm.io/install

2) Download and install experimental version to your local Sandstorm:
https://github.com/wekan/wekan/wiki/Sandstorm
Local sandstorm is at http://local.sandstorm.io:6080/ .

3) Download your production Wekan grain .zip file with down arrow button. Upload to your dev local Sandstorm.
Try does it work.
