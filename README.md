# Traefik setup

This will setup an instance of traefik that I use as reverse-proxy for other docker projects

## Folder structure

```
traefik/
    acme.json
    .env
    docker-compose.yml
```

## Environment

Duplicate the `.env.template` file and rename it to `.env`

```
LETSENCRYPT_EMAIL=
TRAEFIK_HOST=<traefik.domain.com>
TRAEFIK_DASHBOARD_USERNAME=
TRAEFIK_DASHBOARD_PASSWORD=
SERVER_IP=
```

`LETSENCRYPT_EMAIL` is the email used to generate the SSL
`TRAEFIK_HOST` and `TRAEFIK_DASHBOARD_` are used to access Traefik dashboard

To generate the `TRAEFIX_DASHBOARD_PASSWORD`, use following commands

```
sudo apt-get install apache2-utils
htpasswd -nb <username> <secure_password>
```

`SERVER_IP` is used if you use [pi-hole](https://github.com/tmssd/kb-tpl-docker-pihole).
If you're using [Wireguard](https://github.com/tmssd/kb-tpl-wireguard), use the Wireguard server IP here.

## acme.json

Before running, you need to create a `acme.json` file and change its permissions:

```
touch acme.json
chmod 600 acme.json
```

## Create network

```
docker network create web
```

## Start the container

```
docker-compose build && docker-compose up -d
```
