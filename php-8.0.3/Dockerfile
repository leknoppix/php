FROM php:8.0.3-fpm-buster

ENV PHP_SECURITY_CHECHER_VERSION=1.0.0

RUN apt-get update && apt-get install -y \
    wget \
    git \
    libzip-dev \
    libicu-dev \
    p7zip-full \
    libmagickwand-dev --no-install-recommends

RUN docker-php-ext-install pdo zip intl opcache mysqli pdo_mysql

RUN pecl install apcu imagick redis

RUN docker-php-ext-enable redis apcu

COPY --from=composer /usr/bin/composer /usr/bin/composer

ADD ./php-8.0.3/php.ini /usr/local/etc/php/conf.d/

RUN wget https://get.symfony.com/cli/installer -O - | bash \
    && mv /root/.symfony/bin/symfony /usr/local/bin/symfony \
    && git config --global user.email "your@email.fr" \
    && git config --global user.name "your name"

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /var/www

EXPOSE 9000
