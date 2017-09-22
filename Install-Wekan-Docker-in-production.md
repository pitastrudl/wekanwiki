**Purpose:** run Wekan on a production Linux server with Docker and Apache or Nginx as a front-end server (reverse proxy)

## 1. Install Docker and Docker-compose

[Install Docker](http://docs.docker.com/linux/step_one/) and 
[install Docker-Compose](http://docs.docker.com/compose/install/).
* Docker-Compose: 
```bash
curl -L https://github.com/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
```
```
chmod +x /usr/local/bin/docker-compose
```


## 2. Configure Wekan

* Let say we create a dedicated user for Wekan : `sudo useradd -d /home/wekan -m -s /bin/bash wekan`
* Add this user to the docker group: `sudo usermod -aG docker wekan`
* Create the file `/home/wekan/docker-compose.yml` containing following.
* CHANGE ROOT_URL https://example.com TO YOUR REAL WEKAN URL LIKE http://example.com , http://example.com/wekan , http://IP-ADDRESS-HERE OR SIMILAR.


```yaml
version: '2'

services:

  wekandb:
    image: mongo:3.2.14
    container_name: wekan-db
    command: mongod --smallfiles --oplogSize 128
    networks:
      - wekan-tier
    expose:
      - 27017
    volumes:
      - wekan-db:/data/db
      - wekan-db-dump:/dump

  wekan:
    image: wekanteam/wekan:latest
    container_name: wekan-app
    networks:
      - wekan-tier
    ports:
      - 8081:80
    environment:
      - MONGO_URL=mongodb://wekandb:27017/wekan
      - ROOT_URL=http://example.com
      - MAIL_URL=smtp://user:pass@mailserver.example.com:25/
      - MAIL_FROM=wekan-admin@example.com
    depends_on:
      - wekandb

volumes:
  wekan-db:
    driver: local
  wekan-db-dump:
    driver: local

networks:
  wekan-tier:
    driver: bridge
```

**Note:** we want to preserve the port 80 on the host, so we bind Wekan on port 8081. This port 8081 will next be bound to a vhost in apache (thus on port 80).

**Note:** to start the wekan containers automatically on boot, use the `restart: always` policy on both containers. e.g.
  ```
  wekan:
    image: wekanteam/wekan:latest
    restart: always
    ...

  wekandb:
    image: mongo:3.2.12
    restart: always
    ...
  ```

**Info:** Default DB user: wekandb. Default DB name: wekan.

## 3. Configure Mail Server
You can choose to _NOT_ configure a mail server, by not providing the `MAIL_URL` & `MAIL_FROM` environment parameters. Instead the mail message will be send to the terminal output. See [FAQ](https://github.com/wekan/wekan/wiki/FAQ#show-mails-with-a-docker-image-without-mail-configuration) for more info.

If you want to configure a mail server, you could use a mail server out-side of your machine (like the example  above). Or you could start another Docker container which runs Postfix (try the [`marvambass/versatile-postfix`](https://hub.docker.com/r/marvambass/versatile-postfix/) Docker image).

If you already got a Postfix service running on your host machine, you can add the local IP address to the docker-compose.yml file and use the hostname in the `MAIL_URL`:
```
environment:
  [...]
 - MAIL_URL=smtp://mailserver
 - MAIL_FROM=noreply@domain.com
extra_hosts:
 - "mailserver:192.168.1.20"
```
**Note:** `192.168.1.20` needs to be changed to your local server IP address.

And finally add the Docker IP range (172.17.x.x) to the Postfix trusted networks list in `/etc/postfix/main.cf`:
```
mynetworks = 127.0.0.0/8 172.17.0.0/16 [::ffff:127.0.0.0]/104 [::1]/128  
```

## 4. Configure webserver as a front-end proxy
### 4.a Apache 

* Enable Mod_Proxy: `sudo a2enmod proxy proxy_http proxy_wstunnel` then restart Apache `service apache2 restart`
* Configure your virtual host (vhost)

Let say you have the following "mytodo.org" vhost configured in `/etc/apache2/sites-available/mytodo.org.conf`:

```ApacheConf
<VirtualHost *:80>
        ServerName mytodo.org
        ServerAdmin webmaster@mytodo.org

        DocumentRoot /var/www-vhosts/mytodo.org
        <Directory />
                Options FollowSymLinks
                AllowOverride AuthConfig FileInfo Indexes Options=MultiViews
        </Directory>

        <Directory /var/www-vhosts/mytodo.org>
                Options -Indexes +FollowSymLinks +MultiViews
                AllowOverride AuthConfig FileInfo Indexes Options=MultiViews
                Require all granted
        </Directory>

        ErrorLog /var/log/apache2/mytodo.org-error.log

        # Possible values include: debug, info, notice, warn, error, crit,
        # alert, emerg.
        LogLevel warn

        CustomLog /var/log/apache2/mytodo.org-access.log combined
        ServerSignature Off
</VirtualHost>
```

Add the following lines at the end just before `</VirtualHost>`:

```ApacheConf
        ProxyPassMatch   "^/(sockjs\/.*\/websocket)$" "ws://127.0.0.1:8081/$1"
        ProxyPass        "/" "http://127.0.0.1:8081/"
        ProxyPassReverse "/" "http://127.0.0.1:8081/"
```

**Note:** if not already done, don't forget to enable your vhost `sudo a2ensite mytodo.org`

Reload Apache `sudo service apache2 reload`

[Apache Mod_Proxy documentation](http://httpd.apache.org/docs/current/mod/mod_proxy.html)

### 4.b nginx

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