FROM php:8.0-fpm
COPY php.ini /usr/local/etc/php/

RUN apt-get update \
  && apt-get install -y git openssh-client zlib1g-dev mariadb-client vim libzip-dev libpq-dev libonig-dev zip unzip \
  && docker-php-ext-install zip pdo_pgsql mbstring bcmath

# PHP実行・デバッグで必要なライブラリをインストール
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

#Composer install
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1

ENV COMPOSER_HOME /composer

ENV PATH $PATH:/composer/vendor/bin


#WORKDIR /var/www
WORKDIR /workspace

RUN composer global require "laravel/installer"