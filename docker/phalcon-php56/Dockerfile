FROM php:5.6-fpm
RUN apt-get update && apt-get install -y \
        gcc make autoconf libc-dev pkg-config git \
        openssl \
        libpcre3-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        zlib1g-dev \
        libmemcached-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt bcmath \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include --with-jpeg-dir=/usr/include \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysqli \
    # Install php-memcached
    && pecl install memcached-2.2.0 \
    && docker-php-ext-enable memcached \
    # Install redis
    && pecl install redis \
    && docker-php-ext-enable redis \
    && pecl install xdebug-2.5.5 \
    && docker-php-ext-enable xdebug \
    # Install phalcon.so
    && git clone https://github.com/phalcon/cphalcon \
    && cd cphalcon/build && ./install \
    && docker-php-ext-enable phalcon \
    && cd ../.. && rm -rf cphalcon \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*
