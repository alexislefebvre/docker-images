FROM php:7.1-cli-alpine

ENV COMPOSER_ALLOW_SUPERUSER=1

# copy Composer from official image
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# git and unzip are necessary for Composer, mysql-client will install “mysqldump” command
RUN apk add --no-cache git unzip mysql-client \
 && apk add --no-cache freetype-dev libjpeg-turbo-dev libpng-dev \
 && docker-php-ext-install -j$(nproc) iconv \
 && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
 && docker-php-ext-install -j$(nproc) gd \
 && docker-php-ext-install pdo_mysql
