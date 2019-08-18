#FROM php:${PHP_VERSION:+${PHP_VERSION}-}fpm-alpine AS my_php
#FROM php:fpm-alpine AS deps

#COPY --from=composer /usr/bin/composer /usr/bin/composer



#FROM alpine
FROM vimagick/openssh

RUN apk add --no-cache bash

#RUN mkdir /var/run/sshd
#RUN sed -i 's/#PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config

RUN adduser www-data -h /var/www -s /bin/bash -D; \
    echo "www-data:www-data" | chpasswd; \
    mkdir -p /var/www/html/public; \
    chown -R www-data:www-data /var/www;



#COPY --from=deps /var/www /var/www



## Composer (which composer)
##COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=dockerlampalpine_php /usr/bin/composer /usr/bin/composer

## Php (which php, php -i | grep extension_dir)
##COPY --from=php:fpm-alpine /usr/local/bin/php /usr/local/bin/php
COPY --from=dockerlamp_php /usr/local/bin/php /usr/local/bin/php
COPY --from=dockerlamp_php /usr/lib /usr/lib

##RUN apk add --no-cache php7 php-common php-cli php-mbstring php-bz2 php-phar
#RUN apk add --no-cache php-phar php-mbstring
##RUN docker-php-ext-install phar
#RUN apk add --no-cach openssl
##RUN docker-php-ext-install openssl


#WORKDIR /var/www/html
#ENTRYPOINT  ["/bin/bash"]
#ENTRYPOINT  ["/bin/sh"]
#ENTRYPOINT ["/entrypoint.sh"]
#VOLUME /root
#USER user
#EXPOSE 22
#CMD ["/usr/sbin/sshd", "-D"]


#FROM alpine:3.8
#RUN apk add --no-cache sudo bash openssh && \
#    addgroup -S user && \
#    adduser -S -D user -G user && \
#    echo "root:root" | chpasswd && \
#    echo "user:root123" | chpasswd && \
#    echo "user ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/user && \
#    sed -i '/user/s/false/ash/g' /etc/passwd && \
#    sed -i s/#PermitRootLogin./PermitRootLogin\ yes/ /etc/ssh/sshd_config && \
#    rm -rf /var/cache/apk/ && \
#    rm -rf /tmp/* && \
#    ssh-keygen -A
#USER user
#EXPOSE 22
#CMD ["/usr/sbin/sshd", "-D"]