**Purpose:** run Wekan on a production Linux server with Docker and Apache as a front-end (reverse proxy)

## 1. Install Docker and Docker-compose

[Install Docker](http://docs.docker.com/linux/step_one/) and [install Docker-Compose](http://docs.docker.com/compose/install/).

## 2. Configure Wekan

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
  ports:
    - 8081:80

wekandb:
   image: mongo
   volumes:
     - /home/wekan/data:/data/db
```

**Note:** we want to preserve the port 80 on the host, so we bind Wekan on port 8081. This port 8081 will next be bound to a vhost in apache (thus on port 80).

## 3. Configure Apache as a front-end proxy

* Enable Mod_Proxy: `sudo a2enmod proxy proxy_http` then restart Apache `service apache2 restart`
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
        ProxyPass        "/" "http://127.0.0.1:8081/"
        ProxyPassReverse "/" "http://127.0.0.1:8081/"
```

**Note:** if not already done, don't forget to enable your vhost `sudo a2ensite mytodo.org`

Reload Apache `sudo service apache2 reload`

[Apache Mod_Proxy documentation](http://httpd.apache.org/docs/current/mod/mod_proxy.html)

## 4. Launch Wekan on boot
