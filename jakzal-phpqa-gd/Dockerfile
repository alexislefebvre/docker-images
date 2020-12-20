FROM jakzal/phpqa:php7.4-alpine

RUN apk add --no-cache freetype-dev libjpeg-turbo-dev libpng-dev \
 && docker-php-ext-install -j$(nproc) iconv \
 && docker-php-ext-configure gd --with-freetype --with-jpeg \
 && docker-php-ext-install -j$(nproc) gd
