## 1) Enable Mod_Proxy

```
sudo a2enmod proxy proxy_http proxy_wstunnel
```

[Apache Mod_Proxy documentation](http://httpd.apache.org/docs/current/mod/mod_proxy.html)

## 2) Restart Apache

Systemd:
```
sudo systemctl restart apache2
```
Init.d:
```
sudo service apache2 restart
```

## 3) Enable SSL in Apache config
```
Listen 443

NameVirtualHost *:443
```
## 4) Set Apache proxy

SSL with [Certbot](https://certbot.eff.org).

Config at `/etc/apache2/sites-available/example.com.conf`:

```ApacheConf
<VirtualHost *:443>

    SSLEngine On
    SSLCertificateFile      /etc/letsencrypt/live/example.com/cert.pem
    SSLCertificateKeyFile   /etc/letsencrypt/live/example.com/privkey.pem
    SSLCertificateChainFile /etc/letsencrypt/live/example.com/chain.pem

    ProxyPassMatch   "^/(sockjs\/.*\/websocket)$" "ws://127.0.0.1:3001/$1"
    ProxyPass        "/" "http://127.0.0.1:3001/"
    ProxyPassReverse "/" "http://127.0.0.1:3001/"

</VirtualHost>
```

## 5) Enable your site

```
sudo a2ensite example.com
```
Or, add symlink manually:
```
sudo su

cd /etc/apache2/sites-enabled

ln -s ../sites-available/example.com.conf example.com.conf
```

## 6) Reload Apache

Systemd:
```
sudo systemctl restart apache2
```
Init.d:
```
sudo service apache2 restart
```

## 7) Snap settings
```
sudo snap set wekan root-url='https://example.com'

sudo snap set wekan port='3001'
```
[More snap settings keys](https://github.com/wekan/wekan-snap/wiki/Supported-settings-keys)