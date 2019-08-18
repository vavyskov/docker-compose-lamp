## https://hub.docker.com/r/aexchecker/docker-php/dockerfile/
## https://hub.docker.com/r/wodby/drupal-php/dockerfile/

ARG PHP_VERSION=""

FROM php:${PHP_VERSION:+${PHP_VERSION}-}fpm-alpine AS my_php

RUN apk update; \
    apk upgrade

## PHP extension: MySQL, MariaDB, Percona Server, or equivalent
## (Wordpress: mysqli, Drupal: pdo_mysqli)
RUN docker-php-ext-install mysqli pdo_mysql

## PHP extension: opcache
RUN docker-php-ext-install opcache

## PHP extension: gd
##Next librarires: libjpeg-turbo-dev libwebp-dev zlib-dev libxpm-dev
RUN apk add --no-cache libpng libpng-dev; \
    docker-php-ext-install gd; \
    apk del libpng-dev

## PHP extension: PECL uploadprogress
RUN apk add --no-cache git; \
    git clone https://github.com/php/pecl-php-uploadprogress/ /usr/src/php/ext/uploadprogress/; \
    docker-php-ext-install uploadprogress; \
    apk del git

## Composer (which composer)
COPY --from=composer /usr/bin/composer /usr/bin/composer
