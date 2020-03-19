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
