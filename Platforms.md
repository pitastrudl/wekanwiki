# Supported

* Source-based platforms
* [Sandstorm](https://sandstorm.io), [making .spk packages](https://github.com/wekan/wekan/issues/823)
* [Autoinstall script][autoinstall]
* [Docker Compose: Wekan <=> MongoDB](https://github.com/wekan/wekan-mongodb)
* [Docker Compose: Alpine Linux and Wekan <=> MongoDB](https://github.com/wekan/wekan-launchpad)
* [Docker Compose: Wekan <=> MongoDB <=> ToroDB => PostgreSQL](https://github.com/wekan/wekan-postgresql)
* [Docker Development](https://github.com/wekan/wekan-dev)
* [Virtual appliance](https://github.com/wekan/wekan/wiki/virtual-appliance)
* Heroku
  * Email to work on already working Heroku: Use 3rd party email like SendGrid, update process.env.MAIL_URL ,
change from email at Accounts.emailTeamplates.from , new file in server folder called smtp.js on code
`Meteor.startup(function () });` . TODO: Test and find a way to use API keys instead.

# Upcoming

Support will be added after upgrading to Meteor 1.4 and Node v4.

* [Ubuntu 14.04](https://github.com/wekan/wekan/issues/978)
* [Windows](https://github.com/wekan/wekan/issues/977)

# Not tested yet

* Azure: Install from source or Docker. Azure endpoint needs to be added.
* OpenShift
* Google Cloud: Needs info how to enable websockets.