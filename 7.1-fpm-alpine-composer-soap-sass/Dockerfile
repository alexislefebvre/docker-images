FROM ruby:2.4-alpine as ruby
RUN apk add --no-cache build-base libffi-dev
RUN gem install sass

FROM php:7.1-fpm-alpine

ENV COMPOSER_ALLOW_SUPERUSER=1

COPY --from=composer /usr/bin/composer /usr/local/bin/composer

ENV APCU_VERSION 5.1.8

RUN apk add --no-cache ca-certificates icu-libs git unzip zlib-dev
RUN apk add --no-cache --virtual .build-deps $PHPIZE_DEPS icu-dev
RUN apk add --no-cache freetype libpng libjpeg libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev

# For “SoapClient”
RUN apk add --no-cache libxml2-dev

RUN docker-php-ext-install intl zip exif
RUN docker-php-ext-install -j$(nproc) iconv
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd
RUN pecl install apcu-${APCU_VERSION}
RUN docker-php-ext-enable apcu
RUN docker-php-ext-enable opcache
RUN docker-php-ext-enable exif
RUN docker-php-ext-install pdo_mysql

# For “SoapClient”
RUN docker-php-ext-install soap
# For “app/console server:start” command
RUN docker-php-ext-install pcntl

RUN echo "short_open_tag = off" >> /usr/local/etc/php/php.ini
RUN echo "memory_limit = -1" >> /usr/local/etc/php/php.ini
RUN echo "date.timezone = Europe/Paris" >> /usr/local/etc/php/conf.d/symfony.ini
RUN echo "opcache.max_accelerated_files = 20000" >> /usr/local/etc/php/conf.d/symfony.ini
RUN echo "realpath_cache_size=4096K" >> /usr/local/etc/php/conf.d/symfony.ini
RUN echo "realpath_cache_ttl=600" >> /usr/local/etc/php/conf.d/symfony.ini
RUN echo "memory_limit = -1" >> /usr/local/etc/php/conf.d/symfony.ini
RUN apk del .build-deps
RUN apk add gosu --update --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ --allow-untrusted
RUN addgroup bar
RUN adduser -D -h /home -s /bin/sh -G bar foo

RUN apk add --no-cache ruby && ruby -v

COPY --from=ruby /usr/local/bundle/ /usr/local/bundle/
RUN ruby /usr/local/bundle/gems/sass-3.7.3/bin/sass --version

ADD entrypoint.sh /entrypoint

ENTRYPOINT ["/entrypoint"]
