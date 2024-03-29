FROM php:7.4-fpm

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
    install-php-extensions gd apcu bcmath exif gettext imagick pcntl \
    intl ldap mcrypt mysqli opcache pdo_mysql redis soap sockets zip

RUN apt-get autoremove --purge -y && apt-get autoclean -y && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* /var/tmp/* \
    && locale-gen

COPY --from=composer /usr/bin/composer /usr/bin/composer

ADD ./php-7.4/php.ini /usr/local/etc/php/conf.d/

WORKDIR /var/www

EXPOSE 9000