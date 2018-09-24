FROM php:5.6.36-fpm

RUN apt-get update && apt-get install -y \
                libfreetype6-dev \
                libjpeg62-turbo-dev \
                #mcrypt====
                autoconf \
                libc-dev \
                pkg-config \
                libmcrypt-dev \
                #==================
                libpng-dev \
                ca-certificates \
                curl \
                git \
                wget \
                lynx \
                wkhtmltopdf \
                libldb-dev \
                libldap2-dev \
                libsasl2-dev \
                zip \
                libpq-dev \
                libzip-dev \
                libbz2-dev \
                libgd2-dev \
                libjpeg-dev \
                libgif-dev \
                libxml2-dev \
                apt-utils \
                supervisor \
                && docker-php-ext-install -j$(nproc) pdo_mysql mysqli \
                && docker-php-ext-install -j$(nproc) exif hash gettext sockets ctype xml zip pcntl \
                && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/  \
                && docker-php-ext-install -j$(nproc) gd \
                && docker-php-ext-install mcrypt \
                && pecl install xdebug-2.5.5 \
                install redis \
                && docker-php-ext-enable xdebug \
                && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
                && rm -rf /var/lib/apt/lists/* \
                && rm -rf /tmp/pear

# Add configuration files
COPY ./conf/php-xdebug-enabled.ini /usr/local/etc/php/conf.d/xdebug-enabled.ini

EXPOSE 9000
CMD ["php-fpm"]
