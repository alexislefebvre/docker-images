FROM php:7.2-cli-alpine

ENV COMPOSER_ALLOW_SUPERUSER=1

# copy Composer from official image
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# git and unzip are necessary for Composer
RUN apk add --no-cache git libpng-dev unzip
RUN docker-php-ext-install gd
