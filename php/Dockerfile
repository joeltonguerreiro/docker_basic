FROM php:7.4-fpm

RUN apt update && apt install -y vim libpq-dev git unzip libzip-dev libpng-dev \ 
    libjpeg-dev libfreetype6-dev libxml2-dev redis-server iputils-ping iproute2 python python3-pip \
    librdkafka-dev libgmp-dev supervisor \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql pdo_mysql mysqli\
    && docker-php-ext-enable pdo_mysql \
    && curl --silent --show-error https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && docker-php-ext-install zip \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install exif \
    && docker-php-ext-install xmlwriter \
    && docker-php-ext-install simplexml \
    && docker-php-ext-install sockets \
    && docker-php-ext-install gmp \
    && docker-php-ext-install bcmath

RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd

RUN pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis

RUN redis-server --daemonize yes

# KAFKA
#RUN pecl install rdkafka \
#    && echo "extension=rdkafka.so" > /usr/local/etc/php/conf.d/rdkafka.ini

#RUN pip3 install supervisor

# debug
RUN pecl install -o -f xdebug-3.1.5 \
    && docker-php-ext-enable xdebug

# Install NewRelic
COPY newrelic_init /usr/bin/newrelic_init
COPY newrelic_install /usr/bin/newrelic_install

RUN /usr/bin/newrelic_install
RUN /usr/bin/newrelic_init