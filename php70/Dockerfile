FROM mhart/alpine-node

MAINTAINER Gilberto Junior <olamundo@gmail.com>

#####################################
# Enviroments Variables:
#####################################
ENV HOME="/root" \
    PATH=$HOME/.yarn/bin:$PATH \
    COMPOSER_HOME=$HOME/composer

#####################################
# Libs:
#####################################
RUN apk add --no-cache curl git vim bash

#####################################
# PHP 7.0:
#####################################
RUN wget -O /etc/apk/keys/php-alpine.rsa.pub \
    http://php.codecasts.rocks/php-alpine.rsa.pub && \
    echo "http://php.codecasts.rocks/7.0" >> /etc/apk/repositories && \
    apk add --update php7 \
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
        php7-phar \
        php7-opcache \
        php7-openssl \
        php7-zlib \
        php7-xdebug

RUN ln -sf /usr/bin/php7 /usr/bin/php

#####################################
# Composer:
#####################################
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/bin/composer && \
    chmod +x /usr/bin/composer

#####################################
# BASHRC:
#####################################
RUN touch /root/.bashrc

#####################################
# Yarn:
#####################################
RUN curl -o- -L https://yarnpkg.com/install.sh | bash

#####################################
# Workdir
#####################################
RUN mkdir -p /var/www/html

#####################################
# User docker:
#####################################
RUN addgroup -g 1000 docker && \
    adduser -u 1000 -h /home/docker -D -G docker docker && \
    chown -R docker:docker /var/www/html && \
    chown -R docker:docker /home/docker

#####################################
# Final:
#####################################
RUN rm -rf /var/cache/apk/* /tmp/* /usr/share/man

USER docker
WORKDIR /var/www/html

CMD ["bash"]
