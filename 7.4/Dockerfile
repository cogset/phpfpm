FROM php:7.4-fpm

RUN set -eux; \
        \
        apt-get update; \
        apt-get install -y --no-install-recommends \
                cron \
                git \
                procps \
                libfreetype6-dev \
                libjpeg-dev \
                libpng-dev \
                libssl-dev \
                libwebp-dev \
                libzip-dev \
                openssl \
                supervisor \
                unzip \
                zip \
        ; \
        rm -r /var/lib/apt/lists/*

RUN set -eux; \
        \
        docker-php-ext-configure gd \
                --with-freetype-dir=/usr/include/ \
                --with-jpeg-dir=/usr/include/ \
                --with-webp-dir=/usr/include/ \
        ; \
        docker-php-ext-install \
                gd \
                pcntl \
                pdo_mysql \
                sockets \
                zip \
        ; \
        pecl install redis; \
        docker-php-ext-enable redis

RUN set -eux; \
        \
        curl -L https://getcomposer.org/installer | php; \
        mv composer.phar /usr/local/bin/composer

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["php-fpm"]
