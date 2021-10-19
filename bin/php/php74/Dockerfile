FROM php:7.4-apache-buster

MAINTAINER rtsarkov

# Install
RUN apt-get -y update && \
    apt-get -y --no-install-recommends install \
        nano \
        wget \
        default-mysql-client \
        libzip-dev \
        libicu-dev \
        git \
        curl \
        libonig-dev \
        libcurl4 \
        libcurl4-openssl-dev \
        zip \
        openssl && \
    rm -rf /var/lib/apt/lists/* && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug-2.8.0 && \
    docker-php-ext-enable xdebug

# Install imagick
RUN apt-get update && \
    apt-get -y --no-install-recommends install --fix-missing libmagickwand-dev && \
    rm -rf /var/lib/apt/lists/* && \
    pecl install imagick && \
    docker-php-ext-enable imagick

# Other PHP7 Extensions
RUN docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install curl && \
    docker-php-ext-install tokenizer && \
    docker-php-ext-install json && \
    docker-php-ext-install zip && \
    docker-php-ext-install -j$(nproc) intl && \
    docker-php-ext-install mbstring

RUN docker-php-ext-install opcache

# Enable apache modules
RUN a2enmod rewrite headers

# Cleanup
RUN rm -rf /usr/src/*
