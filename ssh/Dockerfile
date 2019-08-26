## Multi-stage builds

ARG PHP_FROM=vavyskov/php:7.2-fpm-alpine
ARG COMPOSER_FROM=vavyskov/php:7.2-fpm-alpine

FROM ${PHP_FROM} AS php
FROM ${COMPOSER_FROM} AS composer
FROM alpine

ENV USER_NAME=www-data
ENV USER_PASSWORD=www-data
ENV USER_GROUP=www-data
ENV USER_HOME=/var/www

RUN apk add --no-cache \
        openssh-server \
        bash \
## Prevents unwanted restarting of the container (when using the docker-compose.yml)
&&  ssh-keygen -A

## Php (get path command: which php, php -i | grep extension_dir)
COPY --from=php /usr/local/bin/php /usr/local/bin/php
COPY --from=php /usr/lib /usr/lib

## Composer (get path command: which composer)
COPY --from=composer /usr/bin/composer /usr/bin/composer

#VOLUME ${USER_HOME}/html

## Initialize container
COPY config/entrypoint.sh /usr/local/bin/
RUN chmod u+x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
