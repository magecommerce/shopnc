FROM php:7.2-fpm
RUN apt-get update && apt-get install -y \
        gcc make autoconf libc-dev pkg-config unzip \
        openssl \
        libpcre3-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        zlib1g-dev \
        libmemcached-dev \
    && docker-php-ext-install -j$(nproc) iconv bcmath \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include --with-jpeg-dir=/usr/include \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql \
    # Install php-memcached
    && pecl install memcached \
    && docker-php-ext-enable memcached \
    # Install redis
    && pecl install redis \
    && docker-php-ext-enable redis \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    # Install phalcon.so
    && curl -LO https://resource.baiyjk.com/php/cphalcon-3.3.x.zip \
    && unzip cphalcon-3.3.x.zip && cd cphalcon-3.3.x/build && ./install \
    && docker-php-ext-enable phalcon \
    && cd ../.. && rm -rf cphalcon-3.3.x \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*
