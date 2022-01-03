FROM php:7.4-fpm

ENV PHP_SECURITY_CHECHER_VERSION=1.0.0

RUN apt-get update && apt-get install -y \
    wget \
    git \
    libzip-dev \
    libicu-dev \
    7z \
    libmagickwand-dev --no-install-recommends

RUN docker-php-ext-install pdo zip intl opcache mysqli pdo_mysql apcu imagick

RUN pecl install apcu && pecl install imagick redis

COPY --from=composer /usr/bin/composer /usr/bin/composer

ADD ./php-7.4/php.ini /usr/local/etc/php/conf.d/

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /var/www

EXPOSE 9000
