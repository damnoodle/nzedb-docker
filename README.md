**This project is forked from, and is no longer maintained by, razorgirl. This repo is for my personal use. As such, everything is untested and surly broken!!!. Only changes are newer versions of alpine linux and packages.**

# nzedb-docker

A Dockerfile to create a full [nZEDb](https://github.com/nZEDb/nZEDb) install in one go. It's intended to make setting up and testing nZEDb quick and painless.

Based on:

* Alpine Linux 3.14
* MariaDB 10.5.13-r0
* PHP 7.4.26-r0
* nginx/1.20.2-r0

Most extras get installed, including `htop`, `vnstat`, `bwm-ng`, `mytop`, `memcached`, `ffmpeg`, `mediainfo`, `p7zip`, `unrar` and `lame`.

## Installation

You need to have [Docker](http://www.docker.com/) installed. If you don't or are not familiar with Docker, please take a look at their web site. They do a really good job of getting you up and running.

### Build

```
docker-compose build
```

### Create services and start

```
docker-compose up
```

### Stop

```
docker-compose stop
```

### Start

```
docker-compose start
```

### Destroy

```
docker-compose down
```

### Info

In a new terminal run `docker-compose ps`. The output will be similar to this:

```
        Name                      Command             State           Ports
------------------------------------------------------------------------------------
nzedbdocker_mariadb_1   docker-entrypoint.sh mysqld   Up      3306/tcp
nzedbdocker_nginx_1     nginx                         Up      0.0.0.0:8800->8800/tcp
nzedbdocker_nzedb_1     /run.sh                       Up
nzedbdocker_php_1       php-fpm                       Up      9000/tcp
```

Note the ports. `0.0.0.0:8800->8800/tcp` means that port 8800 from inside the container forwards to the same on your host. Thus, you can connect to the nZEDb interface via port 8800. Assuming you're running Docker on the same machine you're working on, open your browser with the URL `http://<HOST_IP>:8800/install`.

For more options on running and managing Docker containers, please consult the [Docker User Guide](https://docs.docker.com/userguide/).

### MariaDB

MariaDB is configured with the following users:

```
root / nzedb
nzedb / nzedb
```

### Timezone

You should probably adjust your timezone. Change it in `php/php.ini` and `nzedb/Dockerfile` before building the images.

## Notes

As Docker is 64-bit only, you need to have current hardware.
