FROM php:8.3-cli-alpine

ENV COMPOSER_ALLOW_SUPERUSER=1

# copy Composer from official image
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# git and unzip are necessary for Composer, mysql-client will install “mysqldump” command
RUN apk add --no-cache git unzip mysql-client \
  && docker-php-ext-install pdo_mysql

RUN apk add --no-cache --virtual .build-deps $PHPIZE_DEPS icu-dev \
 && apk add --no-cache libintl \
 && docker-php-ext-install intl

# necessary for code coverage
RUN apk add --no-cache autoconf gcc g++ make \
 && pecl install pcov && docker-php-ext-enable pcov \
 && echo "pcov.enabled=0" >> $PHP_INI_DIR/php.ini
