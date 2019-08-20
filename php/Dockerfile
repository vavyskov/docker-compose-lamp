## https://hub.docker.com/r/aexchecker/docker-php/dockerfile/
## https://hub.docker.com/r/wodby/drupal-php/dockerfile/

ARG PHP_VERSION=""

FROM php:${PHP_VERSION:+${PHP_VERSION}-}fpm-alpine

## PHP extension: MySQL, MariaDB, Percona Server, or equivalent (Wordpress: mysqli, Drupal: pdo_mysqli)
RUN docker-php-ext-install mysqli pdo_mysql \
## PHP extension: opcache
&&  docker-php-ext-install opcache \
## PHP extension: gd (next librarires: libjpeg-turbo-dev libwebp-dev zlib-dev libxpm-dev)
&&  apk add --no-cache libpng libpng-dev \
&&  docker-php-ext-install gd \
&&  apk del libpng-dev \
## PHP extension: PECL uploadprogress
&&  apk add --no-cache git \
&&  git clone https://github.com/php/pecl-php-uploadprogress/ /usr/src/php/ext/uploadprogress/ \
&&  docker-php-ext-install uploadprogress \
&&  apk del git

## Composer (get path command: which composer)
#COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
