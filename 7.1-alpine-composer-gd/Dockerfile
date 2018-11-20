# use composer from official image
FROM composer:latest as composer

FROM php:7.1-cli-alpine
ENV COMPOSER_ALLOW_SUPERUSER=1
# copy Composer from official image
COPY --from=composer /usr/bin/composer /usr/bin/composer
# add plugin then remove cache
RUN composer global require "hirak/prestissimo:^0.3" \
 && rm -rf /root/.composer/cache

# git and unzip are necessary for Composer
RUN apk add --no-cache git unzip \
 && apk add --no-cache freetype-dev libjpeg-turbo-dev libpng-dev \
 && docker-php-ext-install -j$(nproc) iconv \
 && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
 && docker-php-ext-install -j$(nproc) gd \
 && docker-php-ext-install pdo_mysql
