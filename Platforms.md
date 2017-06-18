2017-05-31 [SECURITY FLAW IN ADMIN PANEL](https://github.com/wekan/wekan/issues/1048).

# Updated often

Automatic generated newest builds are available for Docker, and platforms that
install directly from this repo. Automatic builds will be added later for more
platforms.

First registered Wekan user will get [Admin Panel][features] on new
Docker and source based installs. You can also
[enable Admin Panel manually](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v0111-rc2-2017-03-05-wekan-prerelease).

You may need these on other platforms than Sandstorm:
* [Troubleshooting Mail](https://github.com/wekan/wekan/wiki/Troubleshooting-Mail)
* [Troubleshooting CentOS 7](https://github.com/wekan/wekan/issues/718)
* [Nginx webserver config](https://github.com/wekan/wekan/wiki/Nginx-Webserver-Config)
* [Nginx workaround](https://github.com/wekan/wekan/issues/1015)
* [Caddy webserver config](https://github.com/wekan/wekan/wiki/Caddy-Webserver-Config)
* [Bug: Some modules not using ROOT_URL](https://github.com/wekan/wekan/issues/973)


### Docker

[Docker Compose: Wekan <=> MongoDB](https://github.com/wekan/wekan-mongodb)

[Cleanup and delete all Docker data to get Docker Compose working](https://github.com/wekan/wekan/issues/985)

More info:

[Install via Docker](https://github.com/wekan/wekan/wiki/Docker)

### Source

[Install from source][install_source]

### VirtualBox

[Virtual appliance](https://github.com/wekan/wekan/wiki/virtual-appliance)

### Cloudron

[![Install on Cloudron][cloudron_button]][cloudron_install]

[Wekan package for deployment on a server with Cloudron installed](https://cloudron.io/store/io.wekan.cloudronapp.html)

[Package repo](https://git.cloudron.io/cloudron/wekan-app)

### Ubuntu snap

[Install Ubuntu snap](https://github.com/wekan/wekan-snap)

# Updated once a month

### Indiehosters

[![SignUp][indiehosters_button]][indiehosters_saas]

# Updated sometimes

### Sandstorm

[![Try on Sandstorm][sandstorm_button]][sandstorm_appdemo]

https://sandstorm.io

[Downloading latest .spk package file](https://github.com/wekan/wekan/issues/998)

[Sandstorm](https://sandstorm.io), [making .spk packages](https://github.com/wekan/wekan/issues/823)

# Update schedule not known

### Scalingo

[![Deploy to Scalingo][scalingo_button]][scalingo_deploy]

# Could be broken or not up-to-date

### Debian

[Debian Wheezy 64bit & Devuan Jessie 64 bit][debian_wheezy_devuan_jessie]

[Autoinstall script][autoinstall]

### Source on Windows

[Install from source on Windows][installsource_windows], needs [fix for dependencies install error](https://github.com/wekan/wekan/issues/977)

### Uberspace

[Install on Uberspace](https://github.com/wekan/wekan/wiki/Install-latest-Wekan-release-on-Uberspace)

### Heroku 

[![Deploy][heroku_button]][heroku_deploy]

[Heroku deployment quide needed](https://github.com/wekan/wekan/issues/693), [Deploy error](https://github.com/wekan/wekan/issues/638), [Problem with Heroku](https://github.com/wekan/wekan/issues/532)

Email to work on already working Heroku: Use 3rd party email like SendGrid, update process.env.MAIL_URL ,
change from email at Accounts.emailTeamplates.from , new file in server folder called smtp.js on code
`Meteor.startup(function () });` . TODO: Test and find a way to use API keys instead.

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