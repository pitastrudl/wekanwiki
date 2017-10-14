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
