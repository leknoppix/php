FROM php:8.0.3-fpm-buster

ENV PHP_SECURITY_CHECHER_VERSION=1.0.0

RUN apt-get update && apt-get install -y \
    wget \
    git \
    fish

RUN apt-get update && apt-get install -y libzip-dev libicu-dev && docker-php-ext-install pdo zip intl opcache

# Support de apcu
RUN pecl install apcu && docker-php-ext-enable apcu

# Support de redis
RUN pecl install redis && docker-php-ext-enable redis

# Support de MySQL
RUN docker-php-ext-install mysqli pdo_mysql

# Imagick
RUN apt-get update && apt-get install -y libmagickwand-dev --no-install-recommends && pecl install imagick && docker-php-ext-enable imagick

# Composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

# Symfony tool
RUN wget https://get.symfony.com/cli/installer -O - | bash && \
    mv /root/.symfony/bin/symfony /usr/local/bin/symfony

# Security checker tool
RUN curl -L https://github.com/fabpot/local-php-security-checker/releases/download/v${PHP_SECURITY_CHECHER_VERSION}/local-php-security-checker_${PHP_SECURITY_CHECHER_VERSION}_linux_$(dpkg --print-architecture) --output /usr/local/bin/local-php-security-checker && \
    chmod +x /usr/local/bin/local-php-security-checker

ADD ./php-8-0-3-simple/php.ini /usr/local/etc/php/conf.d/

WORKDIR /var/www

EXPOSE 9000
