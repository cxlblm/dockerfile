FROM php:7.4-rc
RUN apt-get update && \
    apt-get install -y \
        procps \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libonig-dev \
        libpng-dev \
        openssl \
        libssl-dev \
        libssh-dev \
        libpcre3 \
        libpcre3-dev \
        libnghttp2-dev \
        libhiredis-dev \
        zlib1g-dev \
        curl \
        zip \
        unzip \
        git \
        wget \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install \
    gd \
    pdo_mysql \
    mbstring \
    json \
    opcache \
    sockets \
    pcntl \
    bcmath \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && echo "opcache.enable_cli=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini \
    && cp "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN cd /root && \
    curl -o /tmp/swoole-releases https://github.com/swoole/swoole-src/releases -L && \
    cat /tmp/swoole-releases | grep 'href=".*archive.*.tar.gz"' | head -1 | \
    awk -F '"' ' {print "curl -o /tmp/swoole.tar.gz https://github.com"$2" -L" > "/tmp/swoole.download"}' && \
    sh /tmp/swoole.download && \
    tar zxvf /tmp/swoole.tar.gz && cd swoole-src* && \
    phpize && \
    ./configure \
    --enable-openssl  \
    --enable-http2  \
    --enable-mysqlnd && \
    make && make install && \
    docker-php-ext-enable swoole && \
    rm -rf /tmp/*