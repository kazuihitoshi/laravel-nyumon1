# docker-laravel 🐳

<p align="center">
    <img src="https://user-images.githubusercontent.com/35098175/145682384-0f531ede-96e0-44c3-a35e-32494bd9af42.png" alt="docker-laravel">
</p>
<p align="center">
    <img src="https://github.com/ucan-lab/docker-laravel/actions/workflows/laravel-create-project.yml/badge.svg" alt="Test laravel-create-project.yml">
    <img src="https://github.com/ucan-lab/docker-laravel/actions/workflows/laravel-git-clone.yml/badge.svg" alt="Test laravel-git-clone.yml">
    <img src="https://img.shields.io/github/license/ucan-lab/docker-laravel" alt="License">
</p>

## Introduction

Build a simple laravel development environment with docker-compose. Compatible with Windows(WSL2), macOS(M1) and Linux.

## Usage

1. Click [Use this template](https://github.com/kazuihitoshi/docker-laravel/generate)
2. Git clone & change directory
3. Execute the following command

```bash
$ make create-project # Install the latest Laravel project
$ make install-recommend-packages # Optional
```

http://localhost

## Tips

- Read this [Makefile](https://github.com/ucan-lab/docker-laravel/blob/main/Makefile).
- Read this [Wiki](https://github.com/ucan-lab/docker-laravel/wiki).

## Container structures

```bash
├── app
├── web
└── db
```

### app container

- Base image
  - [php](https://hub.docker.com/_/php):8.1-fpm-bullseye
  - [composer](https://hub.docker.com/_/composer):2.2

### web container

- Base image
  - [nginx](https://hub.docker.com/_/nginx):1.22

### db container

- Base image
  - [mysql/mysql-server](https://hub.docker.com/r/mysql/mysql-server):8.0

### mailhog container

- Base image
  - [mailhog/mailhog](https://hub.docker.com/r/mailhog/mailhog)
  
### dockerのみでの手動作成

```bash
$ cd docker-laravel && docker-compose up -d

$ docker exec -it docker-laravel_app_1 bash
# usermod www-data -u 1000 && groupmod www-data -g 1000
# exit

$ docker exec -it docker-laravel_web_1 bash
# usermod www-data -u 1000 && groupmod www-data -g 1000
# exit

 1000はホストOSでの自分のuid  app_1は状況により数字部分がカウントアップされている。

$ docker exec -it docker-laravel_app_1 bash
# composer create-project laravel/laravel laravelapp --prefer-dist
# mv laravelapp/* .
# mv laravelapp/.[0-z]* .
# rmdir laravelapp
# chown www-data:www-data -R .
