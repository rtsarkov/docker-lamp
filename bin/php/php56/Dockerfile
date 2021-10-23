FROM php:5.6-apache

MAINTAINER rtsarkov

# Install tools && libraries
RUN apt-get -y update && \
    apt-get -y install \
        nano \
        wget \
        git \
        curl \
        libcurl3 \
        libcurl3-dev \
        zip \
        libmcrypt-dev \
        mysql-client \
        zlib1g-dev \
        libicu-dev \
        libjpeg62-turbo-dev \
        libpng-dev && \
    rm -rf /var/lib/apt/lists/* && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug-2.5.5 && \
    docker-php-ext-enable xdebug

# PHP5 Extensions
RUN docker-php-ext-install curl && \
    docker-php-ext-install tokenizer && \
    docker-php-ext-install json && \
    docker-php-ext-install mcrypt && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install zip && \
    docker-php-ext-install -j$(nproc) intl && \
    docker-php-ext-install mbstring
#    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# Enable apache modules
RUN a2enmod rewrite headers ssl

EXPOSE 80

ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
