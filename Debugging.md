## Finding memory leaks

**[Collect a heap profile and then analyze it](https://github.com/v8/sampling-heap-profiler)**

[Older article: How to Self Detect a Memory Leak in Node](https://www.nearform.com/blog/self-detect-memory-leak-node/)

## 100% CPU usage

1) Increase ulimit system wide to 100 000 in systemd config.

2) Wekan Javascript code has [Node 100% CPU fixes included](https://github.com/wekan/wekan/blob/devel/CHANGELOG.md#v084-2018-04-16-wekan-release). Also read [on-going 100% CPU usage issue progress](https://github.com/meteor/meteor/issues/9796).

3) Newest Wekan includes fixed Node.js binary. Use Fibers fixed [node source from Sandstorm](https://github.com/sandstorm-io/node/commits/sandstorm) or binary [copied from Sandstorm](https://github.com/wekan/wekan-mongodb/issues/2#issuecomment-381453161) or downloaded as node binary or tar.gz package from https://releases.wekan.team , related fixes are in Wekan GitHub repo [Dockerfile](https://github.com/wekan/wekan/blob/devel/Dockerfile), [snapcraft.yaml](https://github.com/wekan/wekan/blob/devel/snapcraft.yaml) and [wekan/server/authentication.js](https://github.com/wekan/wekan/blob/devel/server/authentication.js). 

## Scaling to thousands of users

[Production setup at AWS](https://github.com/wekan/wekan/wiki/AWS)

## Current versions of dependencies

[Dockerfile](https://github.com/wekan/wekan/blob/devel/Dockerfile), versions of Meteor.js, Node etc listed at beginning.

[Included Meteor packages](https://github.com/wekan/wekan/blob/devel/.meteor/packages)

[Included Meteor package versions](https://github.com/wekan/wekan/blob/devel/.meteor/versions)

[Added packages at package.json](https://github.com/wekan/wekan/blob/devel/package.json)

## Build from source

Wekan:
- On any x64 hardware that has Ubuntu 14.04 or Debian 9 or newer installed directly or in VM:
[Build from source scripts](https://github.com/wekan/wekan-maintainer/tree/master/virtualbox)

Wekan for Sandstorm:
- Install above Wekan from source
- Install [Sandstorm locally](https://sandstorm.io/install) with `curl https://install.sandstorm.io | bash`, select dev install
- Install [meteor-spk](https://github.com/sandstorm-io/meteor-spk)
- Get 100% CPU issue fibers fixed node, and copy it to spk directory:<br />
`wget https://releases.wekan.team/node`<br />
`chmod +x node`<br />
`mv node ~/projects/meteor-spk/meteor-spk-0.4.0/meteor-spk.deps/bin/`
- Add to your /home/username/.bashrc : <br /> `export PATH=$PATH:$HOME/projects/meteor-spk/meteor-spk-0.4.0`
- Close and open your terminal, or read settings from .bashrc with<br />`source ~/.bashrc`
- `cd wekan && meteor-spk dev`
- Then Wekan will be visible at local sandstorm at http://local.sandstorm.io:6080/
- Sandstorm commands: `sudo sandstorm`. [Release scripts](https://github.com/wekan/wekan-maintainer/tree/master/releases). Official releases require publishing key that only xet7 has.

Docker:
- `git clone https://github.com/wekan/wekan`
- `cd wekan`
- Edit docker-compose.yml script ROOT_URL etc like documented at https://github.com/wekan/wekan-mongodb docker-compose.yml script
- `docker-compose up -d --build`
