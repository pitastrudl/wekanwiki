* [Docker Compose: Wekan <=> MongoDB](https://github.com/wekan/wekan-mongodb)
* [Docker Compose: Alpine Linux and Wekan <=> MongoDB](https://github.com/wekan/wekan-launchpad)
* [Docker Compose: Wekan <=> MongoDB <=> ToroDB => PostgreSQL](https://github.com/wekan/wekan-postgresql)
* [Docker environment for Wekan Development](https://github.com/wekan/wekan-dev)
* [Docker on SLES12SP1](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-on-SUSE-Linux-Enterprise-Server-12-SP1)

#### Running from remote dockerhub images

Recommended:

* [Wekan <=> MongoDB][wekan_mongodb] - contains the only required Docker Compose file

Development:

* Clone this wekan repo and run from dockerhub without building:

```
sudo docker-compose up -d --nobuild
```

Docker example, running latest Wekan using docker run commands alone:
```
docker run -d --restart=always --name wekan-db mongo:3.4.3

docker run -d --restart=always --name wekan --link "wekan-db:db" -e "MONGO_URL=mongodb://db" -e "ROOT_URL=http://localhost:8080" -p 8080:80 wekanteam/wekan:meteor-1.4
```

#### Running from locally built dockerhub images
```
sudo docker-compose up -d --build
```

#### Running from locally built dockerhub images and modified `ARG` variables (not recommended)
```
echo 'NODE_VERSION=v6.6.0' >> .env && \
echo 'METEOR_RELEASE=1.4.2.3' >> .env && \
echo 'NPM_VERSION=4.1.2' >> .env && \
echo 'ARCHITECTURE=linux-x64' >> .env && \
echo 'SRC_PATH=./' >> .env && \
sudo docker-compose up -d --build
```

