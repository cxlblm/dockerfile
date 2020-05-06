FROM php:latest
RUN apt-get update && \
    apt-get install -y \
        libzip-dev unzip \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) bcmath \
    && docker-php-ext-install -j$(nproc) zip \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && rm -rf /tmp/pear/* \
    && cp "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

WORKDIR /var/www