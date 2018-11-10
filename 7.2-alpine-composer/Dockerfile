# use composer from official image
FROM composer:latest as composer

FROM php:7.2-alpine
ENV COMPOSER_ALLOW_SUPERUSER=1
# copy Composer from official image
COPY --from=0 /usr/bin/composer /usr/bin/composer
# add plugin
RUN composer global require "hirak/prestissimo:^0.3"
# remove cache
RUN rm -rf /root/.composer/cache

# git and unzip are necessary for Composer
RUN apk add --no-cache git libpng-dev unzip
RUN docker-php-ext-install gd
