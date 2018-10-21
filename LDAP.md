## Snap

Snap has [this issue](https://github.com/wekan/wekan-snap/issues/64) that has some info on forum post how to fix it. When it has been fixed, LDAP will be available for Snap. You will see when it's added at https://wekan.github.io ChangeLogs: Edge or Stable.

## Docker

LDAP login works now by using this docker-compose.yml file:
https://raw.githubusercontent.com/wekan/wekan/edge/docker-compose.yml
adding ROOT_URL, LDAP settings etc to that file.

Using this docker-compose:
https://docs.docker.com/compose/install/

With this command:
``` 
docker-compose up -d --no-build
```

## Bugs and Feature Requests

[LDAP Bugs and Feature Requests](https://github.com/wekan/wekan-ldap/issues)
