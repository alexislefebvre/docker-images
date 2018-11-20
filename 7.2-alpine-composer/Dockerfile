# use composer from official image
FROM composer:latest as composer

FROM php:7.2-cli-alpine
ENV COMPOSER_ALLOW_SUPERUSER=1
# copy Composer from official image
COPY --from=composer /usr/bin/composer /usr/bin/composer
# add plugin then remove cache
RUN composer global require "hirak/prestissimo:^0.3" \
 && rm -rf /root/.composer/cache

# git and unzip are necessary for Composer
RUN apk add --no-cache git libpng-dev unzip
RUN docker-php-ext-install gd
