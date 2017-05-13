First registered Wekan user will get Admin Panel on new Docker and source based
installs. You can also [enable Admin Panel manually](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v0111-rc2-2017-03-05-wekan-prerelease)

# Supported

Automatic generated newest builds are available for Docker, and platforms that
install directly from this repo. Automatic builds will be added later for more
platforms.

First registered Wekan user will get [Admin Panel][features] on new
Docker and source based installs. You can also
[enable Admin Panel manually][enable_adminpanel].

[![Deploy][heroku_button]][heroku_deploy]
[![SignUp][indiehosters_button]][indiehosters_saas]
[![Deploy to Scalingo][scalingo_button]][scalingo_deploy]
[![Install on Cloudron][cloudron_button]][cloudron_install]
[![Try on Sandstorm][sandstorm_button]][sandstorm_appdemo]

[VirtualBox][virtualbox]

[Install via Docker](https://github.com/wekan/wekan/wiki/Docker)

[Install from source][install_source]

[Install from source on Windows][installsource_windows]

[Debian Wheezy 64bit & Devuan Jessie 64 bit][debian_wheezy_devuan_jessie]


* [One-click install platforms, cleanup and stats scripts at readme](https://github.com/wekan/wekan#supported-platforms)
* Source-based platforms
* [Sandstorm](https://sandstorm.io), [making .spk packages](https://github.com/wekan/wekan/issues/823)
* [Autoinstall script][autoinstall]
* [Virtual appliance](https://github.com/wekan/wekan/wiki/virtual-appliance)
* [Ubuntu 14.04](https://github.com/wekan/wekan/issues/978)
* Cloudron: [Wekan repo readme](https://github.com/wekan/wekan) has install button for Cloudron. There is also [Wekan package for deployment on a server with Cloudron installed](https://cloudron.io/store/io.wekan.cloudronapp.html) and [package repo](https://git.cloudron.io/cloudron/wekan-app)
* Heroku
* Email to work on already working Heroku: Use 3rd party email like SendGrid, update process.env.MAIL_URL ,
change from email at Accounts.emailTeamplates.from , new file in server folder called smtp.js on code
`Meteor.startup(function () });` . TODO: Test and find a way to use API keys instead.

# Upcoming

Support will be added after upgrading to Meteor 1.4 and Node v4.

* [Windows](https://github.com/wekan/wekan/issues/977)

# Not tested yet

* Azure: Install from source or Docker. Azure endpoint needs to be added.
* OpenShift
* Google Cloud: Needs info how to enable websockets.


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
[virtualbox]: https://github.com/wekan/wekan/wiki/virtual-appliance
[wekan_mongodb]: https://github.com/wekan/wekan-mongodb
[wekan_postgresql]: https://github.com/wekan/wekan-postgresql
[wekan_cleanup]: https://github.com/wekan/wekan-cleanup
[wekan_logstash]: https://github.com/wekan/wekan-logstash
[autoinstall]: https://github.com/wekan/wekan-autoinstall
[autoinstall_issue]: https://github.com/anselal/wekan/issues/18
[debian_wheezy_devuan_jessie]: https://github.com/soohwa/sps/blob/master/example/docs/1/wekan.md
