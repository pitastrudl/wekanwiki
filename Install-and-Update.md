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

### Install Node.js
If you haven't already, you need to install Node.js, given that we need node version 0.10.40, make sure to either use the [custom packages][node-packages] (the ones of your OS are likely too old) or install the correct version from the Node.js [website][node-web].

### Install Meteor
As you might have noticed already, Wekan is built using the Meteor web framework, so we need to install this as well. This can be done easily using their install script ([read it][meteor-script] if you don't trust it):

```sh
# This will install Meteor to ~/.meteor
curl https://install.meteor.com/ | sh
```

### Install MongoDB

In order to run Wekan you need to have MongoDB installed. You can either install your distributions package, if they offer any or see the [MongoDB website][mongodb-website] how to install it.

### Download and build Wekan
First we need to get the latest version of Wekan and change to the cloned folder:

```sh
git clone https://github.com/wekan/wekan.git && cd wekan
```

Now we need to build the meteor app:

```sh
meteor build .build --directory
```
We use `.build` here, as it will be ignored by meteor on subsequent builds, you can as well use a directory outside the libreboard folder.

Now we need to cd into the build server folder and install some dependencies:

```sh
cd .build/bundle/programs/server/ && sudo npm install
```

Now we need to set some environment variables:

```sh
export MONGO_URL='mongodb://127.0.0.1:27017/wekan'
export ROOT_URL='https://example.com'
export MAIL_URL='smtp://user:pass@mailserver.example.com:25/'
export PORT=8080
```

Most of them should be self-explaining. After having set the variables, let's move back to the build package folder and start the server:

```sh
cd ../../
node main.js
```

Done!

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
The first and last line are incase you've installed wekan as a service. Comment them out if not.


[bash-install-script]: https://github.com/anselal/wekan
[virtual-appliance]: https://github.com/anselal/wekan#wekan-virtual-appliance

[contributors-page]: https://github.com/wekan/wekan/blob/devel/Contributing.md#installation
[docker-repo]: https://hub.docker.com/r/mquandalle/wekan/
[sandstorm-guide]: https://sandstorm.io/install/
[node-packages]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[node-web]: https://nodejs.org/download
[meteor-script]: https://install.meteor.com/
[mongodb-website]: https://www.mongodb.org/downloads