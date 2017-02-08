# Install
_Note: Developers looking to contribute to Wekan should follow the instructions on the [Contributors page] [contributors-page] to setup a development environment._

### Installing a new instance of Wekan
There are several options for deploying Wekan. Docker and sandstorm are by far the easiest, but manual installations are supported for those who prefer to customize their installation.

* [Installing with Docker](#install-using-docker)
* [Installing with Sandstorm](#install-with-sandstorm)
* [Installing with Official Binaries](#install-manually-releases)
* [Installing from Source](#install-manually-from-source)

### Upgrading an existing instance

Wekan will automatically migrate your data on first launch. Steps for upgrading depends on the type of installation being upgraded. See the below options.
* [Upgrading Docker](#updating-docker)
* [Upgrading Sandstorm](#updating-sandstorm)
* [Upgrading Manual Installs](#updating-manual-installs)
* [Backing Up Mongo Data](#backup-mongo-data)


***

## Install using Docker
You can install using the official Docker repository located [here][docker-repo].

* [[Install Wekan Docker for testing|Install-Wekan-Docker-for-testing]]
* [[Install Wekan Docker in production|Install-Wekan-Docker-in-production]]

## Install with Sandstorm
Sandstorm is a platform that you can install of your server and it lets you install a variety of apps easily, most of the with a one-click installation.  
For instructions how to install Sandstorm, check out the [guide][sandstorm-guide] on their website! After you have installed Sandstorm, just go to the Admin panel and install the Wekan app! That's all!

## Install manually (Releases)
This is the best option currently if you want to get Wekan running with as few tools as possible. 

There are three options:
 * [Bash Install Script](#bash-install-script)
 * [Virtual Appliance](virtual-appliance)
 * [Manual install](#manual-installation-steps)

## Bash Install Script

You can find a bash installation script at https://github.com/anselal/wekan

## Manual Installation Steps

### Install Node.js

Make sure Node.js is installed (currently Version 0.10.40 is required). If you don't have this version, you can use the [node packages][node-packages].

### Install MongoDB
In order to run Wekan you need to have MongoDB installed. You can either install your distributions package, if they offer any or see the [MongoDB website][mongodb-website] how to install it.

### Install a Wekan release
Now you need to download the release you want to install, usually this is the latest release which you can find [here][latest-release] (you need the `.tar.gz` one).

Extract it:

```sh
tar xzvf wekan-VERSION.tar.gz
```

Move to the server directory and install the dependencies:

```sh
cd wekan-VERSION/bundle/programs/server && sudo npm install
```
Now go back to the base Wekan bundle directory:

```sh
cd ../../
```
Now we just need to make some settings through env variables:

```sh
export MONGO_URL='mongodb://127.0.0.1:27017/wekan'
export ROOT_URL='https://example.com'
export MAIL_URL='smtp://user:pass@mailserver.example.com:25/'
export MAIL_FROM='wekan-admin@example.com'
export PORT=8080
```

Now you are ready to run:

```sh
node main.js
```

Note that it is expected that this command will not exit, and this is not an error.

[latest-release]: https://github.com/wekan/wekan/releases/latest

## Install manually from Source
This is the most complex way, suitable if you know what you are doing and want to have the most flexibility to adapt the installation to your needs. Let's go!

### Notes

If you haven't already, you need to install Node.js, given that we need node version 0.10.40, make sure to either use the [custom packages][node-packages] (the ones of your OS are likely too old) or install the correct version from the Node.js [website][node-web].

* Uses Ubuntu 16.04 VM. You need websockets enabled on your VM.
* For Caddy webserver, ports 80 and 443 need to be open. Caddy has automatic Let's Encrypt,
* for Nginx config you need to configure SSL yourself.

### Install MongoDB

_Note: Installing MongoDB version 3.2.11. This is because 3.4.1 released 2016-12-20 broke something so uploading images did not work, see:
https://github.com/wefork/wekan/issues/58_

```bash
# MongoDB for Ubuntu 16.04
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt update
sudo apt-get install -y mongodb-org=3.2.11 mongodb-org-server=3.2.11 mongodb-org-shell=3.2.11 mongodb-org-mongos=3.2.11 mongodb-org-tools=3.2.11
sudo systemctl start mongod
sudo systemctl enable mongod
```

### Install NodeJS
```bash
# Node.js 0.10.48
sudo apt install build-essential nodejs nodejs-legacy npm git curl
# TODO: Remove -g (if you uninstall npm, globally installed packages are left behind and your package manager doesn't know about them)
sudo npm -g install n
sudo n 0.10.48
sudo npm install npm@latest -g
sudo npm install -g node-gyp
sudo npm install -g fibers
```

### Install Meteor
As you might have noticed already, Wekan is built using the Meteor web framework, so we need to install this as well. This can be done easily using their install script ([read it][meteor-script] if you don't trust it).

However here, we're specifically installing Meteor 1.3.5.1, so follow the instructions below:

```bash
# Meteor 1.3.5.1
mkdir ~/repos
cd ~/repos
git clone --recursive https://github.com/meteor/meteor.git -b release-1.3.5
sudo ln -s ~/repos/meteor/meteor /usr/local/bin/meteor
```

### Install and Build Wekan

```bash
# Wekan
git clone https://github.com/wekan/wekan
cd wekan
#### OPTIONAL: test pull request
##git checkout -b dwrensha-profile-bugfix devel
##git pull https://github.com/dwrensha/wekan.git profile-bugfix
npm install
rm -rf .build
meteor build .build --directory
cd .build/bundle/programs/server
npm install
cd ~/repos
```

## Run Wefork manually

Add to ~/repos/run-wefork.sh

```bash
cd ~/repos/wekan/.build/bundle
export MONGO_URL='mongodb://127.0.0.1:27017/admin'
# Production: https://example.com/wekan
# Local: http://localhost:3000
export ROOT_URL='http://localhost:3000'
export MAIL_URL='smtp://user:pass@mailserver.example.com:25/'
# This is local port where Wekan Node.js runs, same as below on Caddyfile settings.
export PORT=3000
node main.js
```

If you are running it in an IP address, you may need for example
```bash
export ROOT_URL='http://192.168.1.100:3000'
export PORT=3000
```

Make it executeable:
```bash
chmod +x ~/repos/run-wefork.sh
```
You could run it manually with:
```bash
cd ~/repos
./run-wefork.sh
```

Done!

### (Optional) Run Wefork as service

Add to to /etc/systemd/system/wekan@.service

```bash
; see `man systemd.unit` for configuration details
; the man section also explains *specifiers* `%x`

[Unit]
Description=Wekan server %I
Documentation=https://github.com/wefork/wekan
After=network-online.target
Wants=network-online.target
Wants=systemd-networkd-wait-online.service

[Service]
ExecStart=/usr/local/bin/node /home/user/repos/wekan/.build/bundle/main.js
Restart=on-failure
StartLimitInterval=86400
StartLimitBurst=5
RestartSec=10
ExecReload=/bin/kill -USR1 $MAINPID
RestartSec=10
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=Wekan
User=username
Group=username
Environment=NODE_ENV=production
Environment=PWD=/home/username/repos/wekan/.build/bundle
Environment=PORT=3000
Environment=HTTP_FORWARDED_COUNT=1
Environment=MONGO_URL=mongodb://127.0.0.1:27017/admin
Environment=ROOT_URL=https://example.com/wekan
Environment=MAIL_URL='smtp://user:pass@mailserver.example.com:25/'

[Install]
WantedBy=multi-user.target

```

#### To start Wekan and enable service, change to your username where Wekan files are:
```bash
sudo systemctl daemon-reload
sudo systemctl start wekan@username
sudo systemctl enable wekan@username
```

#### To stop Wekan and disable service, change to your username where Wekan files are:
```bash
sudo systemctl daemon-reload
sudo systemctl stop wekan@username
sudo systemctl disable wekan@username
```
Checkout instructions for setup with [[Caddy Webserver Config]] and [[Nginx Webserver Config]] respectively.

# Update


## Updating Docker

If you installed Wekan via Docker, you'll have one Docker container for the database and one container for the application. You'll need to stop the old application container, replace it by the new one and start it again.

See running containers:
```sh
docker ps
```
To stop the running containers:
```sh
docker stop wekan_wekan_1 wekan_wekandb_1
```

Login as the `wekan` user (`su - wekan`), which uses the docker-compose.yml file. To create and start the new container run:
```sh
docker-compose up -d
```
More information about [setup Wekan Docker](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-in-production).

## Updating Sandstorm

Sandstorm updates work automatically. You need to go the the sandstom app market and click on the install button of Wekan. Then Sandstorm will tell you that this application is already installed on your server and ask you if you want to upgrade it.

## Updating Manual Installs

If you installed Wekan manually, you need to stop the Node.js server, download the wekan application and restart the Node.js server.

```sh
sudo systemctl stop wekan@wekan
cd ~/repos/wekan
git pull
npm install
rm -rf .build
meteor build .build --directory
cd .build/bundle/programs/server
npm install
cd ~/repos
sudo systemctl start wekan@wekan
```
The first and last line are incase you've installed [wekan as a service](#optional-run-wefork-as-service). Comment them out if not.

## Backup Mongo Data

```sh
#!/bin/bash
now=$(date +'%Y-%m-%d_%H.%M.%S')
mkdir -p backups/$now
cd backups/$now
mongodump
cd ..
zip -r $now.zip $now
cd ../..
echo "\nBACKUP DONE."
echo "Backup is at directory backups/${now}."
echo "Backup is also archived to .zip file backups/${now}.zip"
```


[bash-install-script]: https://github.com/anselal/wekan
[virtual-appliance]: https://github.com/anselal/wekan#wekan-virtual-appliance

[contributors-page]: https://github.com/wekan/wekan/blob/devel/Contributing.md#installation
[docker-repo]: https://hub.docker.com/r/mquandalle/wekan/
[sandstorm-guide]: https://sandstorm.io/install/
[node-packages]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[node-web]: https://nodejs.org/download
[meteor-script]: https://install.meteor.com/
[mongodb-website]: https://www.mongodb.org/downloads