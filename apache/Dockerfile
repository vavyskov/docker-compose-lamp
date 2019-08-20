ARG APACHE_VERSION=""

FROM httpd:${APACHE_VERSION:+${APACHE_VERSION}-}alpine

## Copy apache vhost file to proxy php requests into php-fpm container
COPY config/proxy.apache.conf /usr/local/apache2/conf/proxy.apache.conf

## Append configuration
RUN echo "Include /usr/local/apache2/conf/proxy.apache.conf" \
        >> /usr/local/apache2/conf/httpd.conf \
## Enable clean URLs
&&  sed -i '/LoadModule rewrite_module/s/^#//g' /usr/local/apache2/conf/httpd.conf
