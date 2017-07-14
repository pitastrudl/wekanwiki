## Docker Hub

Currently there are two dockerhub builds for wekan. One at [mquandalle dockerhub](https://hub.docker.com/r/mquandalle/wekan/builds/) and another at [wekanteam dockerhub](https://hub.docker.com/r/wekanteam/wekan/builds/). 

For now, [wekanteam dockerhub](https://hub.docker.com/r/wekanteam/wekan/builds/) is recommended as it supports tagged releases. There is a separate `docker-compose.yml` for [wekanteam dockerhub](https://hub.docker.com/r/wekanteam/wekan/builds/) at [this repo link](https://github.com/wekan/wekan-mongodb) with instructions on installing there also.

## Quay

[![Docker Repository on Quay](https://quay.io/repository/wekan/wekan/status "Docker Repository on Quay")](https://quay.io/repository/wekan/wekan)

[Many tags available](https://quay.io/repository/wekan/wekan?tab=tags)

Example:
```
docker run -d --restart=always --name wekan-db mongo:3.2.14

docker run -d --restart=always --name wekan --link "wekan-db:db" -e "MONGO_URL=mongodb://db" -e "ROOT_URL=http://localhost:8080" -p 8080:80 quay.io/wekan/wekan:latest
```

Added 2017-05-06 to see if it has better debugging of failed builds than Docker Hub.

## Development:

### `docker run` examples

- No build step and pull from the [mquandalle dockerhub](https://hub.docker.com/r/mquandalle/wekan/builds/)
```
docker run -d --restart=always --name wekan-db mongo:3.2.14
```

- No build step, pull from the [wekanteam dockerhub](https://hub.docker.com/r/wekanteam/wekan/builds/) and
specify docker variables
```
docker run -d --restart=always --name wekan --link "wekan-db:db" -e "MONGO_URL=mongodb://db" -e "ROOT_URL=http://localhost:8080" -p 8080:80 wekanteam/wekan:latest
```

### `docker-compose` examples

- No build step and pull from the [mquandalle dockerhub](https://hub.docker.com/r/mquandalle/wekan/builds/)

```
sudo docker-compose up -d --nobuild
```

- Build default
```
sudo docker-compose up -d --build
```

- Build with newer Node version:
```
echo 'NODE_VERSION=v6.8.1' >> .env && \
sudo docker-compose up -d --build
```

- Build custom image off a release candidate or beta for meteor
```
echo 'METEOR_EDGE=1.5-beta.17' >> .env && \
echo 'USE_EDGE=true' >> .env && \
sudo docker-compose up -d --build
```

## Other resources

First registered Wekan user will get Admin Panel on new Docker and source based
installs. You can also [enable Admin Panel manually](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v0111-rc2-2017-03-05-wekan-prerelease)

* [Import/Export MongoDB data to/from Docker container](https://github.com/wekan/wekan/wiki/Export-Docker-Mongo-Data)
* [Cleanup and delete all Docker data to get Docker Compose working](https://github.com/wekan/wekan/issues/985)
* [Docker Compose: Wekan <=> MongoDB](https://github.com/wekan/wekan-mongodb)
* [Docker Compose: Alpine Linux and Wekan <=> MongoDB](https://github.com/wekan/wekan-launchpad)
* [Docker Compose: Wekan <=> MongoDB <=> ToroDB => PostgreSQL](https://github.com/wekan/wekan-postgresql)
* [Docker environment for Wekan Development](https://github.com/wekan/wekan-dev)
* [Docker on SLES12SP1](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-on-SUSE-Linux-Enterprise-Server-12-SP1)
* [Install Wekan Docker for testing. Test mail server. Show mails with a Docker image, without mail configuration](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-for-testing).
* [Install Wekan Docker in production](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-in-production)
* [Caddy Webserver Config](https://github.com/wekan/wekan/wiki/Caddy-Webserver-Config)
* [Nginx Webserver Config](https://github.com/wekan/wekan/wiki/Nginx-Webserver-Config)
* [Move Docker containers to other computer](https://github.com/wekan/wekan/wiki/Move-Docker-containers-to-other-computer), needs more details
