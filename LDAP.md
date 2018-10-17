

LDAP login works now by using this docker-compose.yml file:
https://raw.githubusercontent.com/wekan/wekan/edge/docker-compose.yml
adding ROOT_URL, LDAP settings etc to that file.

Using this docker-compose:
https://docs.docker.com/compose/install/

With this command:
``` 
docker-compose up -d --no-build
```
[LDAP Bugs and Feature Requests](https://github.com/wekan/wekan-ldap/issues)
