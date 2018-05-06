# Install Wekan on SmartOS

based on: https://github.com/greinbold/install-wekan/blob/master/v0.32/freebsd-11.0-RELEASE.md

Used https://github.com/skylime/mi-core-base 1963511a-19d8-4646-90b4-09ecfad1d3ac  core-base 16.4.7

## Prerequisites

Add user `wekan`

	# useradd -m wekan -s /usr/bin/bash

Install prerequisites packages

	# pkgin install mongodb
	## if this failes use
	# pkg_add https://pkgsrc.smartos.skylime.net/packages/SmartOS/2016Q4/x86_64/All/mongodb-3.0.11.tgz
	# pkgin install nodejs curl # 8
	# pkgin install gmake gcc5 git jq # build requirements

Enable MongoDB

	# /usr/sbin/svcadm enable -r svc:/pkgsrc/mongodb:default

## Installation

As wekan

	$ cd
	$ curl https://releases.wekan.team/wekan-0.89.tar.gz  --output wekan-bundle.tar.gz
	$ tar -xzpf wekan-bundle.tar.gz

As root

	# chown -R wekan:wekan /home/wekan/bundle

As wekan

	$ su wekan
	$ cd ~/bundle/programs/server
	$ npm install
	$ export CXX="/opt/local/gcc5/bin/g++ -m64"
	$ export CC="/opt/local/gcc5/bin/gcc -m64"
	$ export CPPFLAGS="-I/opt/local/include"
	$ ln -s /opt/local/bin/node /opt/local/bin/nodejs
	$ npm install fibers@$(jq -r .version < node_modules/fibers/package.json)
	$ cd ~/bundle/programs/server/npm
	$ npm install bson-ext@$(jq -r .version < node_modules/bson-ext/package.json)
	$ # find more packages with native modules: find ~/bundle/ | grep "binding.gyp$"

## Run

Considering that we set the shell for user wekan to `/usr/bin/bash`, the following ENV variables can be set according the following method before starting of Wekan. These must be adapted according the shell.

	$ export MONGO_URL=mongodb://127.0.0.1:27017/wekan
	$ export ROOT_URL=https://example.com
	$ export MAIL_URL=smtp://user:pass@mailserver.example.com:25/
	$ export MAIL_FROM=wekan-admin@example.com
	$ export PORT=8080

Now it can be run

	$ cd ~/bundle
	$ node main.js

## Cleanup

	$ pkgin rm gmake gcc5 git jq # remove build requirements