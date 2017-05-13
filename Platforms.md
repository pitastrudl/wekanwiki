First registered Wekan user will get Admin Panel on new Docker and source based
installs. You can also [enable Admin Panel manually](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v0111-rc2-2017-03-05-wekan-prerelease)

# Supported

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