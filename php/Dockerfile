FROM php:8.1.0-fpm-buster

# COPY php.ini

# Composer install
COPY --from=composer:2.1.12 /usr/bin/composer /usr/bin/composer

# install Node.js
# COPY --from=node:10.22 /usr/local/bin /usr/local/bin
# COPY --from=node:10.22 /usr/local/lib /usr/local/lib
COPY --from=node:17 /usr/local/bin /usr/local/bin
COPY --from=node:17 /usr/local/lib /usr/local/lib

RUN apt-get update && \
  apt-get -y install git libicu-dev libonig-dev libzip-dev unzip locales && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  locale-gen en_US.UTF-8 && \
  localedef -f UTF-8 -i en_US en_US.UTF-8 && \
  mkdir /var/run/php-fpm && \
  docker-php-ext-install intl pdo_mysql zip bcmath && \
  pecl install xdebug && docker-php-ext-enable xdebug && \
  composer config -g process-timeout 3600 && \
  composer config -g repos.packagist composer https://packagist.org

COPY ./php/php.ini /usr/local/etc/php/php.ini

WORKDIR /var/www/html