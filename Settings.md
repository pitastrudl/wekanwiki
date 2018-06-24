Automatic generated newest builds are available for Docker, and platforms that
install directly from this repo. Automatic builds will be added later for more
platforms.

First registered Wekan user will get [Admin Panel](https://github.com/wekan/wekan/wiki/Features) on new
Docker and source based installs. You can also on MongoDB 
[enable Admin Panel](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v0111-rc2-2017-03-05-wekan-prerelease) and [change you as board admin](https://github.com/wekan/wekan/issues/1060#issuecomment-310545976).

You may need these on other platforms than Sandstorm:
* **[Using same database for both LAN and VPN Wekan](https://github.com/wekan/wekan-mongodb/blob/master/docker-compose.yml#L86-L100)**
* [Using Proxy](https://github.com/wekan/wekan/issues/1480)
* [Troubleshooting Mail](https://github.com/wekan/wekan/wiki/Troubleshooting-Mail). For Exchange, you can use [DavMail](http://davmail.sourceforge.net), Wekan SMTP => DavMail => Exchange.
* [Troubleshooting CentOS 7](https://github.com/wekan/wekan/issues/718)
* Webserver config
  * [Nginx](https://github.com/wekan/wekan/wiki/Nginx-Webserver-Config)
  * [Apache](https://github.com/wekan/wekan/wiki/Apache)
  * [Caddy](https://github.com/wekan/wekan/wiki/Caddy-Webserver-Config)
* [RAM usage](https://github.com/wekan/wekan/issues/1088#issuecomment-311843230)