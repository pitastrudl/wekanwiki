**Purpose**: Install Wekan on [Uberspace](https://uberspace.de/) (in userspace on CentOS) and run as daemontools service.

# Option 1:
You can run the commands of the following script step-by-step in the shell. At first step set the SMTP-Password VAR `SMTP_PASS="smtp_password"`. 

# Option 2:
Or you can run it automatically.
* Save it as script (`nano install_wekan.sh`).
* Make it executable (`chmod u+x install_wekan.sh`) 
* Pass the SMTP-Password as command line parameter (`./install_wekan.sh smtp_password`).

```
#!/bin/sh
## 
## Usage: ./install_wekan.sh SMTP-password
##
## Draft
## Install Wekan (v0.10.1 – v0.16) on Uberspace by Noodle
## 
## Sources: 
## https://github.com/wekan/wekan/wiki/Install-and-Update#manual-installation-steps
## https://wiki.uberspace.de/database:mongodb
## https://wiki.uberspace.de/development:nodejs
## https://wiki.uberspace.de/system:daemontools
## https://github.com/wekan/wekan/issues/907


## Set SMTP password
# SMTP_PASS="xxxxxxxxxx"

SMTP_PASS="$1"


#####################
### Setup Node.js ###
#####################

cat <<__EOF__ > ~/.npmrc
prefix = $HOME
umask = 077
__EOF__

echo 'export PATH=/package/host/localhost/nodejs-0.10.43/bin:$PATH' >> ~/.bash_profile
source ~/.bash_profile


#####################
### Setup MongoDB ###
#####################

test -d ~/service || uberspace-setup-svscan
TEMPMDB="$(uberspace-setup-mongodb)"

MONGO_USER="${USER}_mongoadmin"
MONGO_PORT="$(echo ${TEMPMDB} | egrep -o 'm#:\s[0-9]{5}\sUs' | cut -d' ' -f 2)"
MONGO_PASS="$(echo ${TEMPMDB} | egrep -o 'rd:\s.+\sTo\sconn' | cut -d' ' -f 2)"

echo -e "MONGO_USER: ${MONGO_USER} \nMONGO_PORT: ${MONGO_PORT} \nMONGO_PASS: ${MONGO_PASS}"


############################
### Setup Websocket Port ###
############################

export FREE_PORT="$(uberspace-add-port --protocol tcp --firewall | egrep -o '[0-9]{5}')"

echo "FREE_PORT: ${FREE_PORT}"


###################
### Setup Wekan ###
###################

## Issue #907 - Port must be speccified in root url, when Version > 0.10.1
MONGO_URL="mongodb://${MONGO_USER}:${MONGO_PASS}@127.0.0.1:${MONGO_PORT}/wekan?authSource=admin"
ROOT_URL="http://${USER}.${HOSTNAME}:${FREE_PORT}/"
MAIL_URL="smtp://${USER}:${SMTP_PASS}@${HOSTNAME}:587/"
MAIL_FROM="${USER}@${HOSTNAME}"
PORT="${FREE_PORT}"

echo -e "MONGO_URL: ${MONGO_URL} \nPORT: ${PORT} \nROOT_URL: ${ROOT_URL} \nMAIL_URL ${MAIL_URL} \nMAIL_FROM: ${MAIL_FROM}"


#####################
### Install Wekan ###
#####################

mkdir ~/wekan && cd ~/wekan

# Tested versions 0.16  0.13  0.12  0.10.1
WEKAN_VERSION=0.16
curl -OL https://github.com/wekan/wekan/releases/download/v${WEKAN_VERSION}/wekan-${WEKAN_VERSION}.tar.gz && tar xzf wekan-${WEKAN_VERSION}.tar.gz && rm wekan-${WEKAN_VERSION}.tar.gz

cd ~/wekan/bundle/programs/server && npm install
cd ~


#####################
### Setup Service ###
#####################

cat <<__EOF__ >> ~/etc/wekan-setup
#!/bin/bash
export MONGO_URL=${MONGO_URL}
export ROOT_URL=${ROOT_URL}
export MAIL_URL=${MAIL_URL}
export MAIL_FROM=${MAIL_FROM}
export PORT=${PORT}
__EOF__

cat <<__EOF__ >> ~/etc/wekan-start
#!/bin/bash
source ~/etc/wekan-setup
node ~/wekan/bundle/main.js
__EOF__

chmod 700 ~/etc/wekan-setup
chmod a+x ~/etc/wekan-start


## Init & Start as servcie
uberspace-setup-service wekan ~/etc/wekan-start

## Setup & Start in bg for debugging
# source ~/etc/wekan-setup && node ~/wekan/bundle/main.js &


#####################
###    Finish     ###
#####################

echo -e "\n  Login: ${ROOT_URL} \n\n"
```