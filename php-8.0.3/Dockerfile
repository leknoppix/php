FROM php:8.0.3-fpm-buster

ENV PHP_SECURITY_CHECHER_VERSION=1.0.0
ENV COMPOSER_ALLOW_SUPERUSER 0

RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y \
    locales \
    g++ \
    libbz2-dev \
    libmcrypt-dev \
    libc-client-dev \
    libcurl4-gnutls-dev \
    libedit-dev \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libkrb5-dev \
    libldap2-dev \
    libmagickwand-dev \
    libmemcached-dev \
    libpq-dev \
    libsqlite3-dev \
    libssl-dev \
    libreadline-dev \
    libxslt1-dev \
    libzip-dev \
    memcached \
    wget \
    unzip \
    cron \
    zlib1g-dev \
    mariadb-client

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions gd apcu bcmath exif gettext imagick intl ldap mcrypt \
    mongodb mysqli opcache pdo_mysql redis soap sockets zip

RUN apt-get autoremove --purge -y && apt-get autoclean -y && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* /var/tmp/* \
    && locale-gen

COPY --from=composer /usr/bin/composer /usr/bin/composer

ADD ./php-latest/php.ini /usr/local/etc/php/conf.d/

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /var/www

EXPOSE 9000
