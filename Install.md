Welcome to the guide how to install Libreboard on your own Server! There are various ways to do so, just choose one of the following options:

## Install using Docker
You can install using the official Docker repository located [here][docker-repo].

## Install with Sandstorm
Sandstorm is a platform that you can install of your server and it lets you install a variety of apps easily, most of the with a one-click installation.  
For instructions how to install Sandstorm, check out the [guide][sandstorm-guide] on their website! After you have installed Sandstorm, just go to the Admin panel and install the Libreboard app! That's all!

## Install manually
This is the most complex way, suitable if you know what you are doing and want to have the most flexibility to adapt the installation to your needs. Let's go!

### Install Node.js
If you haven't already, you need to install Node.js, given that we need a very recent version, make sure to either use the [custom packages][node-packages] (the ones of your OS are likely too old) or install the latest version from the Node.js [website][node-web].

### Install Meteor
As you might have noticed already, Libreboard is built using the Meteor web framework, so we need to install this as well. This can be done easily using their install script ([read it][meteor-script] if you don't trust it):

```sh
# This will install Meteor to ~/.meteor
curl https://install.meteor.com/ | sh
```

### Install MongoDB

In order to run Libreboard you need to have MongoDB installed. You can either install your distributions package, if they offer any or see the [MongoDB website] how to install it.

### Download and build Libreboard
First we need to get the latest version of Lireboard and change to the cloned folder:

```sh
git clone https://github.com/libreboard/libreboard.git && cd libreboard
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
export MONGO_URL='mongodb://127.0.0.1:27017/libreboard'
export ROOT_URL='https://example.com'
export MAIL_URL='smtp://user:pass@mailserver.example.com:25/'
export PORT=8080
```

Most of them should be self-explaining. After having set the variables, let's move back to the build package folder and start the server:

```sh
cd ../../../
node main.js
```

Done!

[docker-repo]: https://registry.hub.docker.com/u/ncarlier/libreboard/dockerfile/
[sandstorm-guide]: https://sandstorm.io/install/
[node-packages]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[node-web]: https://nodejs.org/download
[meteor-script]: https://install.meteor.com/
[mongodb-website]: https://www.mongodb.org/downloads