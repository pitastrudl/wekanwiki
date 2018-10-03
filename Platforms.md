Downloading and installing Wekan on various platforms.

## Related 

* [Wekan new release ChangeLog](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md)
* [Adding Users](https://github.com/wekan/wekan/wiki/Adding-users)
* [Forgot Password](https://github.com/wekan/wekan/wiki/Forgot-Password)
* [Settings](https://github.com/wekan/wekan/wiki/Settings)
* [Email](https://github.com/wekan/wekan/wiki/Troubleshooting-Mail)
* **[Backup and Restore](https://github.com/wekan/wekan/wiki/Backup) <=== VERY CRITICAL. DO AUTOMATICALLY OFTEN !!**
* [Logs and Stats](https://github.com/wekan/wekan/wiki/Logs)
* [Wekan bug reports and feature requests](https://github.com/wekan/wekan/issues)
* [Proxy](https://github.com/wekan/wekan/issues/1480)


***

## <a name="ProductionSandstorm"></a>Production: Sandstorm platform, many apps and Wekan, security audited, recommended for security critical use on public internet or internal network. Use SaaS or install to your own server. Automatic updates, tested before release. Sandstorm Wekan has different features than Standalone.

Sandstorm is [completely Open Source](https://sandstorm.io/news/2017-02-06-sandstorm-returning-to-community-roots), including [Blackrock Clustering](https://github.com/sandstorm-io/blackrock).

Please support Sandtorm [by subscribing to paid plan](https://sandstorm.io/news/2018-08-27-discontinuing-free-plan). Free plans will be discontinued because there is not enough paid subscribers to pay for server costs. xet7 has spent countless hours to keeping Wekan working on Sandstorm platform, and [many depend on Sandstorm daily. Wekan Team website](https://wekan.team) and [blog](https://blog.wekan.team) run on Sandstorm Oasis, using account paid by xet7. xet7 plans to add more fixes to features to Sandstorm platform. You can also support Wekan on Sandstorm by using [Commercial Support by xet7](https://wekan.team).

Import [does not work](https://github.com/wekan/wekan/issues/1430), needs workarounds. Copying/Moving card to another board [does not work](https://github.com/wekan/wekan/issues/1729). Google/GitHub/LDAP/SAML/Passwordless email login. Free SSL at https://yourservername.sandcats.io domain.

* **[Sandstorm](https://github.com/wekan/wekan/wiki/Sandstorm)** on Debian 64bit, Ubuntu 64bit

***

## Standalone Wekan: Docker, Snap, etc others non-Sandstorm 

Import from Trello, and Import/Export Wekan works. Copying/Moving card to another board works. Password auth. Upcoming: LDAP, OAuth2, etc. Usually for production you just install Ubuntu 18.04 or Debian 9 VM (or without VM) and install Snap. Minimum 2 GB RAM required, preferably 4 GB or more. Requires KVM/XEN/HyperV VM or Bare Metal, where Linux kernel 3.x or 4.x or newer works, and also Snap works without problems. Requires working websockets.

## <a name="ProductionDocker"></a>Production: Docker. No automatic upgrades, use if you have time to test new release first, and it's critical nothing gets broken. Only Standalone Wekan. If security is critical, keep behind firewall, without any ports open to Internet.
* USE
  * Use quay.io image release tags like "1.x" stable.
* DO NOT USE
  * Release tags "1.x.x" edge. They are bleeding edge.
  * Docker Hub images, they are often broken.
* [Docker](https://github.com/wekan/wekan/wiki/Docker)
  * [Windows](https://github.com/wekan/wekan/wiki/Windows)
  * [Mac](https://github.com/wekan/wekan/wiki/Mac)
  * [SLES 64bit](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-on-SUSE-Linux-Enterprise-Server-12-SP1)
* [Proxy](https://github.com/wekan/wekan/issues/1480)

## <a name="ProductionSnap"></a>Production: Snap for Linux, install to your own server or laptop. Automatic Updates. Only Standalone Wekan. If on Snap Stable automatic update breaks something, [report Wekan for Snap bugs and feature requests here](https://github.com/wekan/wekan-snap/issues), so it can be fixed on some automatic update. If security is critical, keep behind firewall, without any ports open to Internet.

* **[Install Snap](https://github.com/wekan/wekan-snap/wiki/Install)** on Linux 64bit. 
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
  * [OpenShift](https://github.com/wekan/wekan/wiki/OpenShift)

## SaaS: Wekan ready services, just start using. Some have free and paid options.

* [Sandstorm](https://github.com/wekan/wekan/wiki/Sandstorm) - Sandstorm Wekan
* [Cloudron](https://github.com/wekan/wekan/wiki/Cloudron) - Standalone Wekan
* [Indiehosters](https://github.com/wekan/wekan/wiki/Indiehosters) - Standalone Wekan
* [Scalingo](https://github.com/wekan/wekan/wiki/Scalingo) - Standalone Wekan

***

## <a name="Development"></a>Development: Not updated automatically.
* [Virtual appliance](https://github.com/wekan/wekan/wiki/virtual-appliance)
* [Source](https://github.com/wekan/wekan/wiki/Source) for development usage only. Source, Snap, Docker, Sandstorm, Meteor bundle and Windows build instructions.
* [Meteor Bundle](https://github.com/wekan/wekan/wiki/Meteor-bundle)
* [Vagrant](https://github.com/wekan/wekan/wiki/Vagrant)
* Upcoming:
  * [EthKan](https://github.com/EthKan) - Snap Standalone Wekan
  * [Friend](https://github.com/wekan/wekan/wiki/Friend) - Snap Standalone Wekan
  * [arm64](https://blog.wekan.team/2018/01/wekan-progress-on-x64-and-arm/index.html) - Snap Standalone Wekan
  * [Snap for other processor architectures](https://github.com/wekan/wekan-snap/issues/46)

## Operating Systems

* [Debian 64bit](https://github.com/wekan/wekan/wiki/Debian)
* [SmartOS](https://github.com/wekan/wekan/wiki/SmartOS)
* [FreeBSD](https://github.com/wekan/wekan/wiki/FreeBSD)

## NAS

* [Qnap TS-469L](https://github.com/wekan/wekan/issues/1180)

## Other Clouds. Can have some restrictions, like: Requires from source install, has restricted 2.x kernel, does not support websockets, or not tested yet.

* [Uberspace](https://github.com/wekan/wekan/wiki/Install-latest-Wekan-release-on-Uberspace)
* [OVH and Kimsufi](https://github.com/wekan/wekan/wiki/OVH)
* [OpenVZ](https://github.com/wekan/wekan/wiki/OpenVZ)
* [Heroku](https://github.com/wekan/wekan/wiki/Heroku) ?
* [Google Cloud](https://github.com/wekan/wekan/wiki/Google-Cloud) ?
* [Cloud Foundry](https://github.com/wekan/wekan/wiki/Cloud-Foundry) ?

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