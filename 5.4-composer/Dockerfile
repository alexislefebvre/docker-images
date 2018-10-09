# use composer from official image
FROM composer:latest as composer

FROM alterway/php:5.4-cli
# for Composer
RUN apt-get update \
    && apt-get install -y zip unzip \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/

ENV COMPOSER_ALLOW_SUPERUSER=1
# copy Composer from official image to replace composer from base image
COPY --from=0 /usr/bin/composer /usr/local/bin/composer
# add plugin
RUN composer global require "hirak/prestissimo:^0.3"
# remove cache
RUN rm -rf /root/.composer/cache

# for some reason, intl extension is not enabled in base image
RUN docker-php-ext-install intl \
    && docker-php-ext-configure intl

# avoir error “Warning: date_default_timezone_get(): It is not safe to rely on the system's timezone settings.”
# source: https://stackoverflow.com/questions/45587214/configure-timezone-in-dockerized-nginx-php-fpm/45587945#45587945
RUN printf '[PHP]\ndate.timezone = "Europe/Paris"\n' > /usr/local/etc/php/conf.d/tzone.ini

# disable entrypoint from base image
ENTRYPOINT []
