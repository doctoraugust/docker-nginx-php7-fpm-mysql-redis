FROM php:7.0-fpm

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    wget \
    git \
    lynx \
    wkhtmltopdf \
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
    && docker-php-ext-install -j$(nproc) iconv mbstring mysqli pdo_mysql zip mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-enable memcached \
    && docker-php-ext-enable redis \
    && docker-php-ext-enable xdebug \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/pear

# Add configuration files
COPY ./conf/php-xdebug-enabled.ini /usr/local/etc/php/conf.d/xdebug-enabled.ini

EXPOSE 9000
