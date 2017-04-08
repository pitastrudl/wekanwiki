First registered Wekan user will get Admin Panel on new Docker and source based
installs. You can also [enable Admin Panel manually](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v0111-rc2-2017-03-05-wekan-prerelease)

* [Import/Export MongoDB data to/from Docker container](https://github.com/wekan/wekan/wiki/Export-Docker-Mongo-Data)
* [Cleanup and delete all Docker data to get Docker Compose working](https://github.com/wekan/wekan/issues/985)
* [Docker Compose: Wekan <=> MongoDB](https://github.com/wekan/wekan-mongodb)
* [Docker Compose: Alpine Linux and Wekan <=> MongoDB](https://github.com/wekan/wekan-launchpad)
* [Docker Compose: Wekan <=> MongoDB <=> ToroDB => PostgreSQL](https://github.com/wekan/wekan-postgresql)
* [Docker environment for Wekan Development](https://github.com/wekan/wekan-dev)
* [Docker on SLES12SP1](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-on-SUSE-Linux-Enterprise-Server-12-SP1)
* [Install Wekan Docker for testing. Test mail server. Show mails with a Docker image, without mail configuration](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-for-testing)
https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-in-production
* [Install Wekan Docker in production](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-in-production)
* [Caddy Webserver Config](https://github.com/wekan/wekan/wiki/Caddy-Webserver-Config)
* [Nginx Webserver Config](https://github.com/wekan/wekan/wiki/Nginx-Webserver-Config)

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
