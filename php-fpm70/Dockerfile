FROM alpine:3.5

MAINTAINER Gilberto Junior <olamundo@gmail.com>

# Environments
ENV TIMEZONE            UTC
ENV PHP_MEMORY_LIMIT    512M
ENV MAX_UPLOAD          50M
ENV PHP_MAX_FILE_UPLOAD 200
ENV PHP_MAX_POST        100M

#####################################
# PHP 7.0:
#####################################
RUN wget -O /etc/apk/keys/php-alpine.rsa.pub \
    http://php.codecasts.rocks/php-alpine.rsa.pub && \
    echo "http://php.codecasts.rocks/7.0" >> /etc/apk/repositories && \
    apk add --update \
        php7 \
        php7-common \
        php7-curl \
        php7-dom \
        php7-json \
        php7-xml \
        php7-mbstring \
        php7-mcrypt \
        php7-pgsql \
        php7-sqlite3 \
        php7-zip \
        php7-bcmath \
        php7-memcached \
        php7-gd \
        php7-dev \
        php7-pdo \
        php7-pdo_mysql \
        php7-pdo_pgsql \
        php7-pdo_sqlite \
        php7-phpdbg \
        php7-memcached \
        php7-redis \
        php7-fpm \
        php7-opcache \
        php7-openssl \
        php7-zlib \
        php7-xdebug

RUN ln /usr/bin/php7 /usr/bin/php

RUN sed -i "s|;*daemonize\s*=\s*yes|daemonize = no|g" /etc/php7/php-fpm.conf && \
    sed -i "s|;*listen\s*=\s*127.0.0.1:9000|listen = 9000|g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;*listen\s*=\s*/||g" /etc/php7/php-fpm.d/www.conf && \
    sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php7/php.ini && \
    sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php7/php.ini && \
    sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|i" /etc/php7/php.ini && \
    sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php7/php.ini && \
    sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php7/php.ini && \
    sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= 0|i" /etc/php7/php.ini

#####################################
# Final:
#####################################
RUN mkdir -p /var/www/html

WORKDIR /var/www/html

ENTRYPOINT ["/usr/sbin/php-fpm7"]
