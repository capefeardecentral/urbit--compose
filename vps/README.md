# Urbit Compose

## VPS

Docker compose configuration to host a local Urbit ship on cloud hardware.

Caddy will reverse proxy your ship and provide TLS.

### init

### VPS

* Point your DNS name to your ip address in your DNS settings
* Update the `Caddyfile` with your domain name
* Ensure ports 80 and 443 are open on your firewall
* Validate your dns is active with `nslookup your.domain.name`

If you need to transfer your key to your vps you can use `scp`

#### comet

Create an empty file with a .comment extension in the urbit directory

```shell
touch urbit/my_name.comet
docker-compose up -d
```

#### planet
copy your planets key file to the urbit directory in this directory

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

### Getting your ship code

Your ship will launch on the docker network port 80. Caddy will reverse proxy this
and if your DNS configuration is correct you will be able to access your ship at
your domain.

generate your code and enter it into the login screen

#### generating urbit code

```shell
docker-compose exec urbit /bin/get-urbit-code
```

#### resetting urbit code

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
