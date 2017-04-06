# Supported

* Source-based platforms
* [Sandstorm](https://sandstorm.io)
* [Virtual appliance](https://github.com/wekan/wekan/wiki/virtual-appliance)
* Meteor 1.4 and Node v4 port on Docker

```
docker run -d --restart=always --name wekan-db mongo:3.4.3

docker run -d --restart=always --name wekan --link "wekan-db:db" -e "MONGO_URL=mongodb://db" -e "ROOT_URL=http://localhost:8080" -p 8080:80 wekanteam/wekan:meteor-1.4
```

# Upcoming

Support will be added after upgrading to Meteor 1.4 and Node v4.

* [Ubuntu 14.04](https://github.com/wekan/wekan/issues/978)
* [Windows](https://github.com/wekan/wekan/issues/977)