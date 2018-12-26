## Docker

- [Docker](https://github.com/wekan/wekan/wiki/Docker)
- [Docker Dev Environment](https://github.com/wekan/wekan-dev)

## Source

1. Install XCode
2. Install [Node 8.14.1](https://nodejs.org/en/)
3. Use [rebuild-wekan.sh script](https://github.com/wekan/wekan/blob/edge/releases/virtualbox/rebuild-wekan.sh) to first install Wekan dependencies and then build Wekan.
4. Change to Wekan directory: `cd wekan`
5. Run meteor: `meteor` - this runs node in http://localhost:3000 and mongo at http://localhost:3001 .
6. Alternatively, to use custom ports, use for example `meteor --port 4000` that runs node in port 4000 and mongo in next port 4001.