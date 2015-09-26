## Wekan with Docker on your own machine

**Purpose**: just to try Wekan on your own Linux workstation

1. [Install Docker](http://docs.docker.com/linux/step_one/)
1. [Install Docker-Compose](http://docs.docker.com/compose/install/)
1. Say we want to save our Wekan data on the host in directory `/home/johndoe/wekan/data`
1. In a given directory (say `/home/johndoe/wekan`), create a `docker-compose.yml` file with:

```yaml
wekan:
  image: mquandalle/wekan
  links:
    - wekandb
  environment:
    - MONGO_URL=mongodb://wekandb/wekan
    - ROOT_URL=http://localhost:80
  ports:
    - 80:80

wekandb:
   image: mongo
   volumes:
     - /home/johndoe/wekan/data:/data/db
```

Then, from the directory containing the `docker-composer.yml` (i.e. `/home/johndoe/wekan`), simply run `docker-compose up`. If you want it to be deamonized, you could run `docker-compose up -d`.

Your wekan data are in `/home/johndoe/wekan/data` and thus can be backed up.

(This procedure has been tested on a Linux Ubuntu 14.04 box.)

## Wekan with Docker + Apache front-end in production

**Purpose:** run Wekan on a production Linux server with Docker and Apache as a front-end (proxy)

### 1. Install Docker and Docker-compose

[Install Docker](http://docs.docker.com/linux/step_one/) and [install Docker-Compose](http://docs.docker.com/compose/install/).

### 2. Configure Wekan

* Let say we create a dedicated user for Wekan : `sudo useradd -d /home/wekan -m -s /bin/bash wekan`.
* Add this user to the docker group: `sudo usermod -aG docker wekan`
* Create the file `/home/wekan/docker-compose.yml` containing: 


```yaml
wekan:
  image: mquandalle/wekan
  links:
    - wekandb
  environment:
    - MONGO_URL=mongodb://wekandb/wekan
    - ROOT_URL=http://localhost:8081

wekandb:
   image: mongo
   volumes:
     - /home/wekan/data:/data/db
```

### 3. Configure Apache as a front-end proxy

* Enable Mod_Proxy: `sudo a2enmod proxy proxy_http` then restart Apache `service apache2 restart`
* Configure your virtual host (vhost)

Let say you have the following vhost:

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
        ProxyPass        "/" "http://127.0.0.1:8081"
        ProxyPassReverse "/" "http://127.0.0.1:8081"
```

and reload Apache `sudo service apache2 reload`

[Apache Mod_Proxy documentation](http://httpd.apache.org/docs/current/mod/mod_proxy.html)

### 4. Launch Wekan on boot
