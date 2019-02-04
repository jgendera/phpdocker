FROM php:7.2-fpm-alpine

RUN apk add --update --no-cache \
    nodejs \
    nodejs-npm \
    libmcrypt-dev \
    libxml2-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    imagemagick-dev \
    autoconf \
    make \
    wget \
    g++ \
    gcc \
    icu \
    icu-dev \
    gnupg

RUN pecl install -o -f redis imagick \
    && docker-php-ext-enable redis opcache imagick \
    && docker-php-ext-configure gd --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure intl

RUN docker-php-ext-install -j$(nproc) pdo_mysql mbstring opcache intl zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY php.ini /usr/local/etc/php

WORKDIR /app