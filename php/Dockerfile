FROM php:7.4-fpm

RUN apt update && apt install -y libpq-dev git unzip libzip-dev libpng-dev\
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql \
    && curl --silent --show-error https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && docker-php-ext-install zip \
    && docker-php-ext-install gd \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install exif
