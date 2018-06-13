FROM php:7.2-fpm

#RUN apt-get update && apt-get install -y \
#curl \
#wget \
#git \
#libfreetype6-dev \
#libjpeg62-turbo-dev \
#libxslt-dev \
#libicu-dev \
#libmcrypt-dev \
#libpng12-dev \
#libxml2-dev \
#&& docker-php-ext-install -j$(nproc) iconv mcrypt mbstring mysqli pdo_mysql zip \
#&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
#&& docker-php-ext-install -j$(nproc) gd

#RUN docker-php-ext-configure intl
#RUN docker-php-ext-install intl
#RUN docker-php-ext-install xsl
#RUN docker-php-ext-install soap
#RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#ADD php.ini /usr/local/etc/php/conf.d/40-custom.ini

RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libxslt-dev \
    libicu-dev \
    libmcrypt-dev \
    libpng-dev \
    libxml2-dev \
    libmemcached-dev \
    zlib1g-dev \
    netcat-openbsd \
    && pecl install -o -f memcached \
    && pecl install redis-4.0.1 \
    && pecl install xdebug-2.6.0 \
    && docker-php-ext-install -j$(nproc) iconv mbstring mysqli pdo_mysql zip \
    && docker-php-ext-enable memcached \
    && docker-php-ext-enable redis \
    && docker-php-ext-enable xdebug \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && rm -rf /tmp/pear

#WORKDIR /var/www
#RUN mkdir public
#RUN echo "<?php phpinfo(); " > public/index.php
#RUN echo "<?php phpinfo(); " > index.php

# Add configuration files
COPY ./conf/php-xdebug-enabled.ini /usr/local/etc/php/conf.d/xdebug-enabled.ini

EXPOSE 9000
