FROM php:7.4-fpm
COPY ./xdebug-2.9.3.tgz /tmp/pear/xdebug-2.9.3.tgz
COPY ./vld-0.17.0.tgz /tmp/pear/vld-0.17.0.tgz

RUN echo "deb http://mirrors.aliyun.com/debian buster main contrib non-free\ndeb http://mirrors.aliyun.com/debian buster-proposed-updates main contrib non-free\ndeb http://mirrors.aliyun.com/debian buster-updates main contrib non-free\ndeb http://mirrors.aliyun.com/debian-security/ buster/updates main non-free contrib" > /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y \
        zlib1g-dev libzip-dev unzip \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) bcmath \
    # && echo "104.236.228.160 pecl.php.net" >> /etc/hosts \
    # && pecl install redis \
    && pecl install /tmp/pear/xdebug-2.9.3.tgz \
    && pecl install /tmp/pear/vld-0.17.0.tgz \
    && docker-php-ext-enable xdebug vld\
    && rm -rf /tmp/pear/* \
    && cp "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"
WORKDIR /var/www