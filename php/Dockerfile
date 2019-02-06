FROM php:7.2.11-fpm

# Install Postgres PDO
RUN apt update && apt install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql