FROM ubuntu:14.04

RUN sed -i 's/http:\/\/archive\.ubuntu\.com\/ubuntu\//http:\/\/mirrors\.aliyun\.com\/ubuntu\//g' /etc/apt/sources.list

RUN echo 'deb http://ppa.launchpad.net/ondrej/php/ubuntu trusty main' > /etc/apt/sources.list.d/php.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E5267A6C
RUN apt-get update

RUN apt-get install -y \
    curl \
    libmemcached-dev \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libpng12-dev \
    libfreetype6-dev \
    libssl-dev \
    libmcrypt-dev \
    libsasl2-dev \
    php7.0-fpm \
    php7.0-mcrypt \
    php7.0-mysql \
    php7.0-gd \
    php7.0-xml \
    php7.0-dev \
    php7.0-zip \
    php7.0-xml \
    php7.0-opcache \
    php7.0-intl \
    php7.0-json \
    php7.0-pgsql \
    php7.0-imap \
    php-pear

RUN mkdir -p /usr/local/openssl/include/openssl/ && \
    ln -s /usr/include/openssl/evp.h /usr/local/openssl/include/openssl/evp.h && \
    mkdir -p /usr/local/openssl/lib/ && \
    ln -s /usr/lib/x86_64-linux-gnu/libssl.a /usr/local/openssl/lib/libssl.a && \
    ln -s /usr/lib/x86_64-linux-gnu/libssl.so /usr/local/openssl/lib/

RUN pecl install mongodb

RUN echo "extension=mongodb.so" > /etc/php/7.0/fpm/conf.d/20-mongodb.ini && \
    chmod 0777 /etc/php/7.0/fpm/conf.d/20-mongodb.ini && \
	echo "extension=mongodb.so" > /etc/php/7.0/mods-available/mongodb.ini

RUN useradd -m -s /bin/bash docker

ADD ./php-fpm.conf /etc/php/7.0/fpm/php-fpm.conf

WORKDIR /var/www
RUN chown -R docker:docker /var/www
CMD /usr/sbin/php-fpm7.0 --nodaemonize
