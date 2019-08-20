FROM alpine

ENV SSH_USER=www-data
ENV SSH_PASSWORD=www-data
ENV SSH_GROUP=www-data
ENV SSH_HOME="/var/www"

RUN apk add --no-cache \
        openssh-server \
        bash \
## Add user
&&  addgroup ${SSH_GROUP} \
&&  adduser -S -D ${SSH_USER} -G ${SSH_GROUP} -h ${SSH_HOME} -s /bin/bash \
&&  echo "${SSH_USER}:${SSH_PASSWORD}" | chpasswd \
&&  mkdir -p ${SSH_HOME}/html/public \
&&  chown -R ${SSH_USER}:${SSH_GROUP} ${SSH_HOME} \
## Prevents unwanted restarting of the container!!!
&&  ssh-keygen -A

## Composer (which composer)
#COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=dockerlamp_php /usr/bin/composer /usr/bin/composer

## Php (which php, php -i | grep extension_dir)
#COPY --from=php:fpm-alpine /usr/local/bin/php /usr/local/bin/php
COPY --from=dockerlamp_php /usr/local/bin/php /usr/local/bin/php
COPY --from=dockerlamp_php /usr/lib /usr/lib

#WORKDIR ${SSH_HOME}/html

#VOLUME ${SSH_HOME}/html

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
