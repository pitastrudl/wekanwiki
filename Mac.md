<img src="https://wekan.github.io/wekan-logo.svg" width="20%" alt="Wekan logo" />

<img src="https://wekan.github.io/MacStadium-developerlogo.png" width="20%" alt="Powered by MacStadium" />

## ChangeLog
- Previously:
  - Below info about Wekan on Mac x64
  - [Wekan PWA on iOS Safari](https://github.com/wekan/wekan/wiki/PWA)
  - Many mobile web fixes
- 2021-05-14 Wekan maintainer [xet7](https://github.com/xet7) got donated hardware [OpenSource MacStadium](https://www.macstadium.com/opensource) remote access to Mac Mini M1 that has 16 GB RAM and 1 TB SSD.
- 2021-05-15 xet7 bought Apple Developer access for 99 euro/year. Trying to figure out how to sign some test app for iPhone, did not get it working yet.
- 2021-05-16 Instructions added below by xet7 about how to run Wekan Server Node.js/MongoDB for development on M1.
- TODO:
  - Trying to find out some way how to make macOS App Store and iOS iPhone/iPad App Store versions of Wekan.
  - [Enable drag handles on iPad landscape mode automatically](https://github.com/wekan/wekan/issues/3755).


## Mac M1 Wekan development

1) Install rosetta:
```
softwareupdate --install-rosetta --agree-to-license
```
2) Clone Wekan:
```
git clone https://github.com/wekan/wekan
cd wekan
```
3) Install Meteor etc
```
curl https://install.meteor.com/ | arch -x86_64 sh
arch -x86_64 meteor npm install --save @babel/runtime
```
3a) Run Meteor on localhost port 4000:
```
WITH_API=true RICHER_CARD_COMMENT_EDITOR=false arch -x86_64 meteor --port 4000
```
3b) Run Meteor on computer IP address on local network port 4000:
```
ROOT_URL=http://192.168.0.100:4000 PORT=4000 WITH_API=true RICHER_CARD_COMMENT_EDITOR=false arch -x86_64 meteor --port 4000
```

## Bundle

1. Install XCode
2. Download wekan-VERSIONNUMBER.zip from https://releases.wekan.team
3. Unzip file you downloaded at step 2. There will be directory called `bundle`.
4. Download [start-wekan.sh script](https://raw.githubusercontent.com/wekan/wekan/master/start-wekan.sh) to directory `bundle` and set it as executeable with `chmod +x start-wekan.sh`
5. Install [Node 12.x](https://nodejs.org/en/)
6. Install [MongoDB 4.x](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)
7. Edit `start-wekan.sh` so that it has for example:
```
export ROOT_URL=http://localhost:2000`
export PORT=2000
export MONGO_URL='mongodb://127.0.0.1:27017/wekan'
```
[More info about ROOT_URL](https://github.com/wekan/wekan/wiki/Settings)

8. Edit `start-wekan.sh` so that it starts in bundle directory command `node main.js`

## Build bundle from source and develop Wekan

1. Install XCode
2. [With steps 3-6 fork and clone your fork of Wekan](https://github.com/wekan/wekan-maintainer/wiki/Developing-Wekan-for-Sandstorm#3-fork-wekan-and-clone-your-fork)

## Docker

- [Repair Docker](https://github.com/wekan/wekan/wiki/Repair-Docker)
- [Docker](https://github.com/wekan/wekan/wiki/Docker)
- [Docker Dev Environment](https://github.com/wekan/wekan-dev)

If you don't need to build Wekan, use prebuilt container with docker-compose.yml from https://github.com/wekan/wekan like this:
```
docker-compose up -d
```

If you like to build from source, clone Wekan repo:
```
git clone https://github.com/wekan/wekan
```
Then edit docker-compose.yml with [these lines uncommented](https://github.com/wekan/wekan/blob/master/docker-compose.yml#L132-L142) this way:
```
   #-------------------------------------------------------------------------------------
    # ==== BUILD wekan-app DOCKER CONTAINER FROM SOURCE, if you uncomment these ====
    # ==== and use commands: docker-compose up -d --build
    build:
      context: .
      dockerfile: Dockerfile
      args:
        - NODE_VERSION=${NODE_VERSION}
        - METEOR_RELEASE=${METEOR_RELEASE}
        - NPM_VERSION=${NPM_VERSION}
        - ARCHITECTURE=${ARCHITECTURE}
        - SRC_PATH=${SRC_PATH}
        - METEOR_EDGE=${METEOR_EDGE}
        - USE_EDGE=${USE_EDGE}
    #-------------------------------------------------------------------------------------
```
Then you can build Wekan with 
```
docker-compose up -d --build
```
