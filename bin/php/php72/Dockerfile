FROM php:7.2-apache-buster

MAINTAINER rtsarkov

RUN apt-get update && \
    apt-get -y --no-install-recommends install \
        nano \
        wget \
        default-mysql-client \
        libzip-dev \
        libicu-dev \
        git \
        curl \
        libcurl4-openssl-dev \
        libcurl4 \
        zip \
        openssl && \
    rm -rf /var/lib/apt/lists/* && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug-2.6.0 && \
    docker-php-ext-enable xdebug

# Other PHP7 Extensions
RUN docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install curl && \
    docker-php-ext-install tokenizer && \
    docker-php-ext-install json && \
    docker-php-ext-install zip && \
    docker-php-ext-install -j$(nproc) intl && \
    docker-php-ext-install mbstring

RUN a2enmod rewrite headers ssl
RUN rm -rf /usr/src/*
