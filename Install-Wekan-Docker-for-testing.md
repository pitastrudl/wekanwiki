**Purpose**: just to try Wekan on your own Linux workstation

1. [Install Docker](http://docs.docker.com/linux/step_one/)
1. [Install Docker-Compose](http://docs.docker.com/compose/install/)
1. Say we want to save our Wekan data on the host in directory `/home/johndoe/wekan/data`
1. In a given directory (say `/home/johndoe/wekan`), create a `docker-compose.yml` file with:

```yaml
wekan:
  image: mquandalle/wekan
  links:
    - wekandb
  environment:
    - MONGO_URL=mongodb://wekandb/wekan
    - ROOT_URL=http://localhost:80
  ports:
    - 80:80

wekandb:
   image: mongo
   volumes:
     - /home/johndoe/wekan/data:/data/db
```

Then, from the directory containing the `docker-compose.yml` (i.e. `/home/johndoe/wekan`), simply run `docker-compose up`. If you want it to be deamonized, you could run `docker-compose up -d`.

Your wekan data are in `/home/johndoe/wekan/data` and thus can be backed up.

**Note**
If the default host port 80 has been used and you would like to set up Wekan for another port, say, 1234, the configuration above
```
  ports:
    - 80:80
```
can be replaced by
```
  ports:
    - 1234:80
```
with all the rest unchanged. 

(This procedure has been tested on Linux Ubuntu 14.04.)

