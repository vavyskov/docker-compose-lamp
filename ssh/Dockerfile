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

## FixMe: Invalid reference format: repository name must be lowercase
#ENV EXTERNAL_PHP_SOURCE=vavyskov/php:${PHP_VERSION:+${PHP_VERSION}-}fpm-alpine
#ENV SOURCE_PHP=php:fpm-alpine
#ENV SOURCE_COMPOSER=composer

## Php (which php, php -i | grep extension_dir)
#COPY --from=php:fpm-alpine /usr/local/bin/php /usr/local/bin/php
#COPY --from=dockerlamp_php /usr/local/bin/php /usr/local/bin/php
#COPY --from=dockerlamp_php /usr/lib /usr/lib
COPY --from=vavyskov/php:7.2-fpm-alpine /usr/local/bin/php /usr/local/bin/php
COPY --from=vavyskov/php:7.2-fpm-alpine /usr/lib /usr/lib

## Composer (which composer)
#COPY --from=composer /usr/bin/composer /usr/bin/composer
#COPY --from=dockerlamp_php /usr/bin/composer /usr/bin/composer
COPY --from=vavyskov/php:7.2-fpm-alpine /usr/bin/composer /usr/bin/composer

#VOLUME ${USER_HOME}/html

## Initialize container
COPY config/entrypoint.sh /usr/local/bin/
RUN chmod u+x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
