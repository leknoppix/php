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
    mariadb-client \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install -j$(nproc) imap \
    && docker-php-ext-configure intl \
    && docker-php-ext-install -j$(nproc) intl \
    && docker-php-ext-install ldap \
    && pecl install mcrypt \
    && docker-php-ext-enable mcrypt \
    && docker-php-ext-install -j$(nproc) \
    bcmath \
    bz2 \
    exif \
    gettext \
    mysqli \
    opcache \
    pdo_mysql \
    pdo_pgsql \
    pgsql \
    soap \
    sockets \
    xsl \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip \
    && pecl install xdebug && docker-php-ext-enable xdebug \
    && pecl install memcached && docker-php-ext-enable memcached \
    && pecl install mongodb && docker-php-ext-enable mongodb \
    && pecl install redis && docker-php-ext-enable redis \
    && docker-php-source delete \
    && apt-get remove -y g++ wget \
    && apt-get autoremove --purge -y && apt-get autoclean -y && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* /var/tmp/* \
    && locale-gen

COPY --from=composer /usr/bin/composer /usr/bin/composer

ADD ./php-7.4/php.ini /usr/local/etc/php/conf.d/

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /var/www

EXPOSE 9000
