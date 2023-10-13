FROM php:8.2-fpm as base

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

RUN apt-get update -y && apt-get install -y git gnupg unzip zip zlib1g-dev libzip-dev
RUN docker-php-ext-install zip

WORKDIR /app


FROM base as dev-runtime

RUN pecl install xdebug
COPY xdebug.ini /usr/local/etc/php/conf.d/99-xdebug.ini

WORKDIR /app
COPY composer.* .
RUN composer install

COPY public/index.php /app/public/index.php
