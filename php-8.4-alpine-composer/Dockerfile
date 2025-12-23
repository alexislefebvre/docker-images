FROM php:8.4.16-cli-alpine AS base

ENV COMPOSER_ALLOW_SUPERUSER=1

# copy Composer from official image
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# git and unzip are necessary for Composer
RUN apk add --no-cache git unzip \
  && docker-php-ext-install opcache pdo_mysql \
  && echo "[opcache]" >> $PHP_INI_DIR/php.ini \
  && echo "opcache.enable=1" >> $PHP_INI_DIR/php.ini

RUN apk add --no-cache --virtual .build-deps $PHPIZE_DEPS icu-dev \
 && apk add --no-cache libintl \
 && docker-php-ext-install intl

# necessary for code coverage
RUN apk add --no-cache autoconf gcc g++ make \
 && pecl install pcov && docker-php-ext-enable pcov \
 && echo "pcov.enabled=0" >> $PHP_INI_DIR/php.ini

FROM base
RUN apk add --no-cache mariadb openjdk11
RUN mkdir --parents /opt/wiremock \
    && curl https://repo1.maven.org/maven2/org/wiremock/wiremock-standalone/3.13.2/wiremock-standalone-3.13.2.jar \
    --output /opt/wiremock/wiremock.jar
RUN java -jar /opt/wiremock/wiremock.jar --version

# TODO:
# - start MariaDB automatically: https://itsfoss.gitlab.io/post/how-to-install-mariadb-on-alpine-linux/
# - configure user and password for MariaDB
# - start WireMock automatically
