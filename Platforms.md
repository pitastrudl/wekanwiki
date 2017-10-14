# Updated often

Automatic generated newest builds are available for Docker, and platforms that
install directly from this repo. Automatic builds will be added later for more
platforms.

First registered Wekan user will get [Admin Panel](https://github.com/wekan/wekan/wiki/Features) on new
Docker and source based installs. You can also on MongoDB 
[enable Admin Panel](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v0111-rc2-2017-03-05-wekan-prerelease) and [change you as board admin](https://github.com/wekan/wekan/issues/1060#issuecomment-310545976).

You may need these on other platforms than Sandstorm:
* **[Using same database for both LAN and VPN Wekan](https://github.com/wekan/wekan-mongodb/blob/master/docker-compose.yml#L86-L100)**
* [Troubleshooting Mail](https://github.com/wekan/wekan/wiki/Troubleshooting-Mail). For Exchange, you can use [DavMail](http://davmail.sourceforge.net), Wekan SMTP => DavMail => Exchange.
* [Troubleshooting CentOS 7](https://github.com/wekan/wekan/issues/718)
* Webserver config
  * [Nginx](https://github.com/wekan/wekan/wiki/Nginx-Webserver-Config)
  * [Apache](https://github.com/wekan/wekan/wiki/Apache)
  * [Caddy](https://github.com/wekan/wekan/wiki/Caddy-Webserver-Config)
* [RAM usage](https://github.com/wekan/wekan/issues/1088#issuecomment-311843230)

### Docker

[Docker Compose: Wekan <=> MongoDB](https://github.com/wekan/wekan-mongodb)

[Docker Compose: Wekan <=> MongoDB <=> ToroDB => PostgreSQL read-only mirroring](https://github.com/wekan/wekan-postgresql)

TODO: [Docker Compose: Wekan <=> MongoDB <=> ToroDB => MySQL read-only mirroring](https://github.com/torodb/stampede/issues/203)

[Cleanup and delete all Docker data to get Docker Compose working](https://github.com/wekan/wekan/issues/985)

More info:

[Install via Docker](https://github.com/wekan/wekan/wiki/Docker)

### Source

[Install from source script for Debian based distros](https://github.com/wekan/wekan-source-installer)

[Install manually from source][install_source]

[Install manually from source without sudo](https://github.com/wekan/wekan/wiki/Install-source-without-sudo-on-Linux)

### VirtualBox

[Virtual appliance](https://github.com/wekan/wekan/wiki/virtual-appliance)

[Scripts from virtual appliance](https://github.com/wekan/wekan-maintainer/tree/master/virtualbox), can be used on any Ubuntu 14.04 64bit install like native or VM. Includes script how to run Node.js on port 80.

### Cloudron

[![Install on Cloudron][cloudron_button]][cloudron_install]

[Wekan package for deployment on a server with Cloudron installed](https://cloudron.io/store/io.wekan.cloudronapp.html)

[Package repo](https://git.cloudron.io/cloudron/wekan-app)

### Ubuntu snap

[Install Ubuntu snap](https://github.com/wekan/wekan-snap/wiki/Install)

[Ubuntu snap bug reports and feature requests](https://github.com/wekan/wekan-snap/issues)

TODO: [Wekan <=> MongoDB <=> ToroDB => MySQL/PosgreSQL read-only mirroring](https://github.com/torodb/stampede/issues/203)

### Sandstorm

[![Try on Sandstorm][sandstorm_button]][sandstorm_appdemo]

[Wekan for Sandstorm Install/Download](https://apps.sandstorm.io/app/m86q05rdvj14yvn78ghaxynqz7u2svw6rnttptxx49g1785cdv1h)

[Sandstorm](https://sandstorm.io)

[Building Wekan for Sandstorm](https://github.com/wekan/wekan-maintainer/wiki/Building-Wekan-for-Sandstorm)

# Updated once a month

### Indiehosters

[![SignUp][indiehosters_button]][indiehosters_saas]

# Updated sometimes

### Qnap TS-469L

[Manual install of newest version](https://github.com/wekan/wekan/issues/1180)

# Update schedule not known

### Scalingo

[![Deploy to Scalingo][scalingo_button]][scalingo_deploy]

# Could be broken or not up-to-date

### Debian

[Debian Wheezy 64bit & Devuan Jessie 64 bit][debian_wheezy_devuan_jessie]

[Autoinstall script][autoinstall]

### Source on Windows

Someone needs to complete instructions about [Install from source on Windows][installsource_windows] to get Wekan running natively on Windows. [git clone on Windows has been fixed](https://github.com/wekan/wekan/issues/977). Related: [running standalone](https://github.com/wekan/wekan/issues/883) and [nexe](https://github.com/wekan/wekan/issues/710).

Somebody should check from Docker website does Linux-based Wekan Docker containers work on Windows. There is also [Docker based development environment for Wekan](https://github.com/wekan/wekan-dev) that is not currently up-to-date, it has been made for faster local Docker builds. See [Dockerfile](https://github.com/wekan/wekan/blob/devel/Dockerfile) about what versions of dependencies are used at Wekan.

### Uberspace

[Install on Uberspace](https://github.com/wekan/wekan/wiki/Install-latest-Wekan-release-on-Uberspace)

### Heroku 

[![Deploy][heroku_button]][heroku_deploy]

[Heroku deployment quide needed](https://github.com/wekan/wekan/issues/693), [Deploy error](https://github.com/wekan/wekan/issues/638), [Problem with Heroku](https://github.com/wekan/wekan/issues/532)

Email to work on already working Heroku: Use 3rd party email like SendGrid, update process.env.MAIL_URL ,
change from email at Accounts.emailTeamplates.from , new file in server folder called smtp.js on code
`Meteor.startup(function () });` . TODO: Test and find a way to use API keys instead.

### Cloud Foundry

[Article from 2016](https://www.cloudfoundry.org/100-day-challenge-082-running-wekan-cloud-foundry/) - probably needs update to use [precompiled Wekan release](https://www.cloudfoundry.org/100-day-challenge-082-running-wekan-cloud-foundry/) ? 

# Not tested yet

* Azure: Install from source or Docker. Azure endpoint needs to be added.
* OpenShift
* Google Cloud: Needs info how to enable websockets.

[install_source]: https://github.com/wekan/wekan/wiki/Install-and-Update#install-manually-from-source
[installsource_windows]: https://github.com/wekan/wekan/wiki/Install-Wekan-from-source-on-Windows
[cloudron_button]: https://cloudron.io/img/button.svg
[cloudron_install]: https://cloudron.io/button.html?app=io.wekan.cloudronapp
[docker_image]: https://hub.docker.com/r/wekanteam/wekan/
[heroku_button]: https://www.herokucdn.com/deploy/button.png
[heroku_deploy]: https://heroku.com/deploy?template=https://github.com/wekan/wekan/tree/master
[indiehosters_button]: https://indie.host/signup.png
[indiehosters_saas]: https://indiehosters.net/shop/product/wekan-20
[sandstorm_button]: https://img.shields.io/badge/try-Wekan%20on%20Sandstorm-783189.svg
[sandstorm_appdemo]: https://demo.sandstorm.io/appdemo/m86q05rdvj14yvn78ghaxynqz7u2svw6rnttptxx49g1785cdv1h
[scalingo_button]: https://cdn.scalingo.com/deploy/button.svg
[scalingo_deploy]: https://my.scalingo.com/deploy?source=https://github.com/wekan/wekan#master
[wekan_mongodb]: https://github.com/wekan/wekan-mongodb
[wekan_postgresql]: https://github.com/wekan/wekan-postgresql
[wekan_cleanup]: https://github.com/wekan/wekan-cleanup
[wekan_logstash]: https://github.com/wekan/wekan-logstash
[autoinstall]: https://github.com/wekan/wekan-autoinstall
[autoinstall_issue]: https://github.com/anselal/wekan/issues/18
[debian_wheezy_devuan_jessie]: https://github.com/wekan/sps

# More

[Features](https://github.com/wekan/wekan/wiki/Features)

[Integrations](https://github.com/wekan/wekan/wiki/Integrations)