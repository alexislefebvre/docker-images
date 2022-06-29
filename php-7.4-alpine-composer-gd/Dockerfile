FROM php:7.4-cli-alpine

ENV COMPOSER_ALLOW_SUPERUSER=1

# copy Composer from official image
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# git and unzip are necessary for Composer, mysql-client will install “mysqldump” command
RUN apk add --no-cache git unzip mysql-client \
 && apk add --no-cache freetype-dev libjpeg-turbo-dev libpng-dev \
 && docker-php-ext-configure gd --with-freetype --with-jpeg \
 && docker-php-ext-install -j$(nproc) gd \
 && docker-php-ext-install pdo_mysql

# necessary for code coverage
RUN apk add --no-cache autoconf gcc g++ make \
 && pecl install pcov && docker-php-ext-enable pcov
