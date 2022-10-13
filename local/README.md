# Urbit Compose

## Local

Docker compose configuration to host a local Urbit ship on your own hardware. 

No TLS or DNS set up required.

### init

#### comet

create an empty file with a .comment extension in the urbit directory

```shell
touch urbit/my.coment
docker-compose up -d
```

#### planet
copy your planets key file to the urbit directory

# NOTE
The portal will give you a key with a numeric suffix. You will need to rename the file to remove the suffix 
or else you get will an error on startup and a comet will be generated

```shell
cp ${MY_KEY_PATH} urbit/${planet-name}.key
docker-compose up -d
```

#### pier
if you have a pier you want to use, copy it to the urbit directory

```shell
cp -r ${MY_PIER_PATH} urbit/${pier-name}
docker-compose up -d
```

### Getting your landscape code

landscape will be available on port 8080 of your host machine

generate your landscape code and enter it into the login screen
    
#### generating landscape code

```shell
docker-compose exec urbit /bin/get-urbit-code
```

#### resetting landscape code

```shell
docker-compose exec urbit /bin/reset-urbit-code
```

### Notes

The official urbit Docker container will default to the root user so any generated pier will be
owned by the root user on your host machine. 

If you do not have root access on your host machine you can create a docker volume to store your pier
and copy the pier with a docker cp command.

```shell
docker-compose cp urbit:/urbit/${pier-name} ${destination}
```
