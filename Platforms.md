Downloading and installing Wekan on various platforms.

## Related 

* [Wekan new release ChangeLog](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md)
* [Settings](https://github.com/wekan/wekan/wiki/Settings)
* [Email](https://github.com/wekan/wekan/wiki/Troubleshooting-Mail)
* [Backup and Restore](https://github.com/wekan/wekan/wiki/Backup)
* [Logs and Stats](https://github.com/wekan/wekan/wiki/Logs)
* [Wekan bug reports and feature requests](https://github.com/wekan/wekan/issues)

## <a name="Production"></a>Production: Snap for Linux, install to your own server or laptop. Automatic Updates. Only Wekan. Supported by xet7.

Import from Trello, and Import/Export Wekan works. Password auth. Upcoming: LDAP, OAuth2, etc. Usually for production you just install Ubuntu 18.04 or Debian 9 VM (or without VM) and install Snap. Requires KVM/XEN/HyperV VM or Bare Metal, where Linux kernel 3.x or 4.x or newer works, and also Snap (or Docker) work without problems. Requires working websockets.

* **[Install Snap](https://github.com/wekan/wekan/wiki/Snap)** on Linux 64bit. [Wekan for Snap bug reports and feature requests](https://github.com/wekan/wekan-snap/issues).
  * **Debian, Ubuntu and Linux Mint based distros**
  * Arch
  * Fedora
  * Solus
  * OpenSUSE
  * Gentoo
  * Manjaro
  * Elementary OS
  * CentOS 7
* Cloud: Some additional info
  * [AWS](https://github.com/wekan/wekan/wiki/AWS)
  * [Azure](https://github.com/wekan/wekan/wiki/Azure)

## <a name="ProductionSandstorm"></a>Production: Sandstorm platform, many apps and Wekan, security audited. Install to your own server. Automatic updates. Supported by xet7.

Import does not work, needs workarounds. Google/GitHub/LDAP/SAML/Passwordless email login. Free SSL at https://yourservername.sandcats.io domain.

* **[Sandstorm](https://github.com/wekan/wekan/wiki/Sandstorm)** on Debian 64bit, Ubuntu 64bit

## SaaS: Wekan ready services, just start using. Some have free and paid options.

* [Sandstorm](https://github.com/wekan/wekan/wiki/Sandstorm)
* [Cloudron](https://github.com/wekan/wekan/wiki/Cloudron)
* [Indiehosters](https://github.com/wekan/wekan/wiki/Indiehosters)
* [Scalingo](https://github.com/wekan/wekan/wiki/Scalingo)

***

## <a name="Development"></a>Development: Only for internal network, not updated automatically.
* [Docker](https://github.com/wekan/wekan/wiki/Docker)
  * [Windows](https://github.com/wekan/wekan/wiki/Windows)
  * [Mac](https://github.com/wekan/wekan/wiki/Mac)
  * [SLES 64bit](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-on-SUSE-Linux-Enterprise-Server-12-SP1)
* [Virtual appliance](https://github.com/wekan/wekan/wiki/virtual-appliance)
* [Source](https://github.com/wekan/wekan/wiki/Source) for development usage only. Source, Snap, Docker, Sandstorm, Meteor bundle and Windows build instructions.
* [Meteor Bundle](https://github.com/wekan/wekan/wiki/Meteor-bundle)
* [Proxy](https://github.com/wekan/wekan/issues/1480)
* [Vagrant](https://github.com/wekan/wekan/wiki/Vagrant)
* Upcoming:
  * [EthKan](https://github.com/EthKan)
  * [Friend](https://github.com/wekan/wekan/wiki/Friend)
  * [arm64](https://blog.wekan.team/2018/01/wekan-progress-on-x64-and-arm/index.html)
  * [Snap for other processor architectures](https://github.com/wekan/wekan-snap/issues/46)

## Operating Systems: For Development only.

* [Debian 64bit](https://github.com/wekan/wekan/wiki/Debian)
* [SmartOS](https://github.com/wekan/wekan/wiki/SmartOS)
* [FreeBSD](https://github.com/wekan/wekan/wiki/FreeBSD)

## NAS: For hobby use

* [Qnap TS-469L](https://github.com/wekan/wekan/issues/1180)

## Cloud: Not supported. Requires from source install, has restricted 2.x kernel, does not support websockets, or not tested yet.

* [Uberspace](https://github.com/wekan/wekan/wiki/Install-latest-Wekan-release-on-Uberspace)
* [OVH and Kimsufi](https://github.com/wekan/wekan/wiki/OVH)
* [OpenVZ](https://github.com/wekan/wekan/wiki/OpenVZ)
* [Heroku](https://github.com/wekan/wekan/wiki/Heroku) ?
* [Google Cloud](https://github.com/wekan/wekan/wiki/Google-Cloud) ?
* [Cloud Foundry](https://github.com/wekan/wekan/wiki/Cloud-Foundry) ?
* [OpenShift](https://github.com/wekan/wekan/wiki/OpenShift) ?

# More

[Features](https://github.com/wekan/wekan/wiki/Features)

[Integrations](https://github.com/wekan/wekan/wiki/Integrations)


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