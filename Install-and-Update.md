# Install
_Note: Developers looking to contribute to Wekan should follow the instructions on [Installing from Source](#install-manually-from-source) to setup a development environment._

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

**Heads up:**
For now this works not on Ubuntu 14.04. You need 16.04 (It needs newer libstdc++ version)

There are three options:
 * [Bash Install Script](#bash-install-script)
 * [Virtual Appliance](virtual-appliance)
 * [Manual install](#manual-installation-steps)

## Bash Install Script

You can find a bash installation script at https://github.com/wekan/wekan-autoinstall

## Manual Installation Steps

### Install Node.js

Make sure Node.js is installed (currently Version 0.10.48 is required). If you don't have this version, you can use the [node packages][node-packages].

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

If you haven't already, you need to install Node.js, given that we need node version 0.10.48, make sure to either use the [custom packages][node-packages] (the ones of your OS are likely too old) or install the correct version from the Node.js [website][node-web].

* Uses Ubuntu 16.04 VM. You need websockets enabled on your VM.
* For Caddy webserver, ports 80 and 443 need to be open. Caddy has automatic Let's Encrypt,
* for Nginx config you need to configure SSL yourself.

### Install MongoDB

_Note: Installing MongoDB version 3.2.x. This is because 3.4.1 released 2016-12-20 broke something so uploading images did not work, see:
https://github.com/wefork/wekan/issues/58_

```bash
# MongoDB for Ubuntu 16.04
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt update
sudo apt install -y mongodb-org mongodb-org-server mongodb-org-shell mongodb-org-mongos mongodb-org-tools
sudo systemctl start mongod
sudo systemctl enable mongod
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
# Download Wekan
git clone https://github.com/wekan/wekan
cd wekan
git submodule init
git submodule update

#### OPTIONAL: test pull request
## git checkout -b dwrensha-profile-bugfix devel
## git pull https://github.com/dwrensha/wekan.git profile-bugfix

# Install Node.js 0.10.48
sudo apt install build-essential nodejs nodejs-legacy npm git curl
sudo npm -g install n 
## if the previous fails (and asks you to run as sudo) just rm /home/<username>/node_modules and retry
sudo n 0.10.48
sudo npm -g install npm@latest
sudo npm -g install node-gyp
sudo npm -g install fibers

# install wekan npm dependancies
npm install
```

#### For Development and Testing
```bash
meteor
```

When running with command `meteor`, any saved modification of HTML/CSS/JS Wekan code
will make changes also on the browser automatically. NPM package C/C++ code is probably
not recompiled though, that needs full rebuild.

#### In production
```bash
rm -rf .build
meteor build .build --directory
cd .build/bundle/programs/server
npm install
cd ~/repos
```

#### Run Wekan manually (if you've built for production)

Add to ~/repos/run-wekan.sh

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

TIP. If you use a public URL for your ROOT_URL instead of a local URL or an IP address make sure the URL is the same when visiting your Wekan URL in your browser for the first time and make sure you add the port number similar to the PORT number you defined. Ie. when visiting your Wekan url like 'http(s)://your-domain.com' this would need a ROOT_URL setting like 'http(s)://your-domain.com:3000'. IF your ROOT_URL setting would be 'http(s)://www.your-domain.com:3000' when visiting the url in your browser without www you will run into url problems when trying to access Card details due to the fact the www is added to he url! The correct ROOT_URL setting is 'http(s)://your-domain.com:3000'.

If you are running it in an IP address, you may need for example
```bash
export ROOT_URL='http://192.168.1.100:3000'
export PORT=3000
```

Make it executeable:
```bash
chmod +x ~/repos/run-wekan.sh
```
You could run it manually with:
```bash
cd ~/repos
./run-wekan.sh
```

Done!

### (Optional) Run Wekan as service

Add to to /etc/systemd/system/wekan@.service

```bash
; see `man systemd.unit` for configuration details
; the man section also explains *specifiers* `%x`
; update <username> with username below

[Unit]
Description=Wekan server %I
Documentation=https://github.com/wekan/wekan
After=network-online.target
Wants=network-online.target
Wants=systemd-networkd-wait-online.service

[Service]
ExecStart=/usr/local/bin/node /home/<username>/repos/wekan/.build/bundle/main.js
Restart=on-failure
StartLimitInterval=86400
StartLimitBurst=5
RestartSec=10
ExecReload=/bin/kill -USR1 $MAINPID
RestartSec=10
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=Wekan
User=<username>
Group=<username>
Environment=NODE_ENV=production
Environment=PWD=/home/<username>/repos/wekan/.build/bundle
Environment=PORT=3000
Environment=HTTP_FORWARDED_COUNT=1
Environment=MONGO_URL=mongodb://127.0.0.1:27017/admin
; https://example.com/wekan for deployment
Environment=ROOT_URL=http://localhost/wekan
Environment=MAIL_URL='smtp://user:pass@mailserver.example.com:25/'

[Install]
WantedBy=multi-user.target

```

#### To start Wekan and enable service, change to your username where Wekan files are:
```bash
sudo systemctl daemon-reload
sudo systemctl start wekan@<username>
sudo systemctl enable wekan@<username>
```

#### To stop Wekan and disable service, change to your username where Wekan files are:
```bash
sudo systemctl daemon-reload
sudo systemctl stop wekan@<username>
sudo systemctl disable wekan@<username>
```
Checkout instructions for setup with [[Caddy Webserver Config]] and [[Nginx Webserver Config]] respectively.

# Update


## Updating Docker

If you installed Wekan via Docker, you'll have one Docker container for the database and one container for the application. You'll need to stop the old application container, replace it by the new one and start it again.

If you have newer Mongo version, you need to backup your MongoDB data (as shown here: [[Export Mongo Data|Export-Docker-Mongo-Data]]) and use similar commands as below to replace your Mongo container with version 3.2.x, and then restore data.

See running containers:
```sh
docker ps
```

To stop the running wekan container (not wekan-db that is MongoDB container):
```sh
docker stop CONTAINER-ID-HERE
```

Remove the container:
```sh
docker rm CONTAINER-ID-HERE
```

See previously downloaded Docker images, that are used to start containers:
```sh
docker images
```

Remove old previously downloaded Docker image:
```sh
docker rmi mquandalle/wekan:latest
```

Download and run latest version:
```sh
docker run -d --restart=always --name wekan --link "wekan-db:db" -e "MONGO_URL=mongodb://db" -e "ROOT_URL=http://localhost:8080" -p 8080:80 mquandalle/wekan:latest
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