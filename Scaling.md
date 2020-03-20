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