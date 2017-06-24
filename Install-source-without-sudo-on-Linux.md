In-progress script for installing npm modules locally. Not tested.

Anyone: If you get this working, edit this wiki and add remaining to be installed locally.

## TODO
- Add MongoDB running locally like at wiki page [Install from source](https://github.com/wekan/wekan/wiki/Install-and-Update#install-mongodb-1)
- Add node.js, npm etc installed locally
- Update [wekan-autoinstall](https://github.com/wekan/wekan-autoinstall), please send pull requests
- Update [Install from source](https://github.com/wekan/wekan/wiki/Install-and-Update#install-mongodb-1) so then this temporary page can possibly be removed later

## Related info
- Node.js and npm version downloaded at [Dockerfile](https://github.com/wekan/wekan/blob/devel/Dockerfile)
- https://gist.github.com/isaacs/579814
- http://linuxbrew.sh

## Only this run with sudo
```
sudo apt-get install build-essential c++ capnproto nodejs nodejs-legacy npm git curl
```

## Install npm modules etc locally
```
# Local node module install from here:
# https://docs.npmjs.com/getting-started/fixing-npm-permissions

# If NPM global package directory does not exists
if [ ! -d "~/.npm-global" ]; then
  # Create it
  mkdir ~/.npm-global
fi

# If .npm-global/bin is in the path
if grep -Fxq "export PATH=~/.npm-global/bin:$PATH" ~/.bashrc
then
    # Continue
else
    # Add it to path
    echo "export PATH=~/.npm-global/bin:$PATH" >> ~/.bashrc
    # Add it to current path in RAM
    export PATH=~/.npm-global/bin:$PATH
fi

# Install packages globally to local ~/.npm-global directory
npm -g install n
npm -g install npm@4.6.1 
npm -g install node-gyp
npm -g install node-pre-gyp
npm -g install fibers@1.0.15

# Install meteor
curl https://install.meteor.com/ | sh

# Install Wekan
cd ~/repos
rm -rf wekan
git clone git@github.com:wekan/wekan.git
cd ~/repos/wekan

# If packages directory does not exists
if [ ! -d "packages" ]; then
  # Create it
  mkdir packages
fi

cd packages
git clone https://github.com/wekan/flow-router.git kadira-flow-router
git clone https://github.com/meteor-useraccounts/core.git meteor-useraccounts-core
cd ~/repos/wekan
rm -rf node_modules
npm install
rm -rf .build
meteor build .build --directory
cp fix-download-unicode/cfs_access-point.txt .build/bundle/programs/server/packages/cfs_access-point.js
cd .build/bundle/programs/server
rm -rf node_modules
npm install
cd ~/repos/wekan
sed -i "s|build\/Release\/bson|browser_build\/bson|g" .build/bundle/programs/server/npm/node_modules/meteor/cfs_gridfs/node_modules/mongodb/node_modules/bson/ext/index.js
cd .build/bundle/programs/server/npm/node_modules/meteor/npm-bcrypt
cd .build/bundle/programs/server/npm/node_modules/meteor/npm-bcrypt
rm -rf node_modules/bcrypt
npm install bcrypt
cd ~/repos
echo Done.
```