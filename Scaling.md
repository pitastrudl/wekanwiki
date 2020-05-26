## Story: MongoDB on bare metal

From tampa:

Hey,

... (about other tries) ...

Last month I threw all this out, recreated all the boards and connected them centrally to a single instance of mongo running on a dedicated server with custom hardware. This was like stepping into the light almost. Since then not a single machine has sent me a mail that it reached 50% usage. It seems insignificant, but the results speak for themselves.

The cloud instances are all shared 1vcpu, 1GB, 10GB storage, they just run wekan natively piped to the background, no docker, no snap, native install. They are connected to the central DB server sitting in the same datacenter. I stuffed a Raid6 with solid disks in that and gave it a hardware controller with a nice big cache. The latency being below 5ms over the network and the DB server having plenty of IO to go around it almost never has a queue of commits going to it and from the cache and IO use I suspect I could grow this tenfold easily.

With this setup each board essentially runs on half the hardware, in terms of cost anyways, yet it works so much better. There seems to be some magic ingredient here, being really fast IO for mongo that reduces system load of wekan by such a large amount that is can practically run even large boards with 40+ concurrent users on the least hardware most cloud providers even offer. With the central server setting up backups has become so much easier, I no longer need to wait for low usage to do backups either.

## Scaling to more users

For any large scale usage, you can:

a) scale with Docker Swarm, etc

b) for big reads or writes, do it on replica

c) for big reads or writes, do it at small amounts at a time, at night, or when database CPU usage seems to be low

Related to docker-compose.yml at https://github.com/wekan/wekan , using Docker Swarm:

[How to scale to more users](https://github.com/wekan/wekan/issues/2711#issuecomment-601163047)

[MongoDB replication docs](https://docs.mongodb.com/manual/replication/)

[MongoDB compatible databases](https://github.com/wekan/wekan/issues/2852)

[AWS](https://github.com/wekan/wekan/wiki/AWS)

[Azure OIDC](https://github.com/wekan/wekan/wiki/Azure)