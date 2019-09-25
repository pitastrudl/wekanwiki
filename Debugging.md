## TODO

[Quote from advise](https://github.com/meteor/meteor/issues/9796#issuecomment-443520767):

> Identify the core service your app is providing and make sure it is running independently. Put everything non-critical, including reporting, on some other system.

[Look at scaling tips here](https://github.com/meteor/meteor/issues/9796#issuecomment-411373831), quote:

> smeijer commented 25 days ago
> Just wanted to let know that I haven't experienced this issue anymore since I've replaced a lot of `meteor publications` with `apollo/graphql requests`.
> 
> The reactivity is thereby lost, but in my case a 30sec poll is also fine. On the places that I do require reactivity, I only `publish` a single `timestamp`. This timestamp is passed through to `apollo`, which triggers a `refetch` when the timestamp is changed.
>
> The [discussion here](https://forums.meteor.com/t/implementing-livedocument-as-an-alternative-to-livequery-discussion/40152) has also been helpfull to improve performance here and there.

[Rocket.Chat scaling tips](https://rocket.chat/docs/installation/manual-installation/multiple-instances-to-improve-performance/)

## Kadira

- https://github.com/edemaine/kadira-compose
- https://github.com/meteor/meteor-apm-agent
- https://github.com/kadira-open/kadira-server
- https://www.gethappyboards.com/2017/07/rolling-out-your-own-instance-of-kadira/

## Finding memory leaks

**[Collect a heap profile and then analyze it](https://github.com/v8/sampling-heap-profiler)**

[Older article: How to Self Detect a Memory Leak in Node](https://www.nearform.com/blog/self-detect-memory-leak-node/)

## 100% CPU usage

1) Increase ulimit system wide to 100 000 in systemd config.

2) Wekan Javascript code has [increaded fiber poolsize](https://github.com/wekan/wekan/blob/master/server/authentication.js#L5-L9).

3) There is [on-going 100% CPU usage Meteor issue](https://github.com/meteor/meteor/issues/9796#issuecomment-400079380) and hopefully [fixes to Node.js will land in Node v8.12](https://github.com/nodejs/node/pull/21593#issuecomment-403636667) sometime. Node 8.12 is now released and official version included at Wekan.

## Scaling to thousands of users

[Production setup at AWS](https://github.com/wekan/wekan/wiki/AWS)

## Current versions of dependencies

[Dockerfile](https://github.com/wekan/wekan/blob/master/Dockerfile), versions of Meteor.js, Node etc listed at beginning.

[Included Meteor packages](https://github.com/wekan/wekan/blob/master/.meteor/packages)

[Included Meteor package versions](https://github.com/wekan/wekan/blob/master/.meteor/versions)

[Added packages at package.json](https://github.com/wekan/wekan/blob/master/package.json)

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