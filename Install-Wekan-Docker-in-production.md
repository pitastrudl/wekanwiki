## Also see: [Using same database for both LAN and VPN Wekan](https://github.com/wekan/wekan/issues/1210)

**Purpose:** run Wekan on a production Linux server with Docker and Apache or Nginx as a front-end server (reverse proxy)

## 1. Install newest Docker and Docker Compose

[Docker website](https://docker.com)

## 2. Use Wekan-MongoDB with Docker Compose

https://github.com/wekan/wekan-mongodb

## 3. Email

[Troubleshooting Email](https://github.com/wekan/wekan/wiki/Troubleshooting-Mail)

## 4. Configure webserver as a front-end proxy

### Nginx

In configuration:

```nginxConf
server {
    listen 123.45.67.89:80;
    server_name mytodo.org;

    access_log  /var/log/nginx/mytodo_access.log;
    error_log   /var/log/nginx/mytodo_error.log;

    [...]
}
```

Add the following after the `error_log` line:

```nginxConf
location / {
   proxy_read_timeout      300;
   proxy_connect_timeout   300;
   proxy_redirect          off;

   proxy_set_header    Host                $http_host;
   proxy_set_header    X-Real-IP           $remote_addr;
   proxy_set_header    X-Forwarded-For     $proxy_add_x_forwarded_for;
   proxy_set_header    X-Forwarded-Proto   $scheme;
      
   proxy_pass http://127.0.0.1:8081;
 }

location ~ websocket$ {
   proxy_pass http://websocket;
   proxy_http_version 1.1;
   proxy_set_header Upgrade $http_upgrade;
   proxy_set_header Connection $connection_upgrade;
}
```

And the following above your `server` line

```nginxConf
upstream websocket {
    server 127.0.0.1:8081;
}

map $http_upgrade $connection_upgrade {
    default upgrade;
    '' close;
}
```


## 5. Launch Wekan

As `wekan` user and from `/home/wekan`, run `docker-compose up -d`

## 6. Improvements to bring to this doc

* Verify everything works


## 7. Tested on...

This procedure has been tested on:

* [VPS-SSD 2016 from OVH](https://www.ovh.com/fr/vps/vps-ssd.xml) with Ubuntu 14.04