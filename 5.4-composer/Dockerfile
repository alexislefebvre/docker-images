# adapted from https://github.com/alterway/docker-php/blob/f1695cc9bb099fcbc2ec5dc104c12b2fa3bb0daa/5.4-cli/Dockerfile

# use composer from official image
FROM composer:latest as composer

FROM php:5.4-cli
# unzip is for Composer, libicu-dev is for internationalization
RUN apt-get update && \
    apt-get install -y \
        libicu-dev \
        unzip && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/

RUN docker-php-ext-install intl && \
    docker-php-ext-configure intl && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install pcntl

ENV COMPOSER_ALLOW_SUPERUSER=1
# copy Composer from official image
COPY --from=composer /usr/bin/composer /usr/local/bin/composer
# add plugin
RUN composer global require "hirak/prestissimo:^0.3"
# remove cache
RUN rm -rf /root/.composer/cache

# avoir error “Warning: date_default_timezone_get(): It is not safe to rely on the system's timezone settings.”
# source: https://stackoverflow.com/questions/45587214/configure-timezone-in-dockerized-nginx-php-fpm/45587945#45587945
RUN printf '[PHP]\ndate.timezone = "Europe/Paris"\n' > /usr/local/etc/php/conf.d/tzone.ini

WORKDIR /app
