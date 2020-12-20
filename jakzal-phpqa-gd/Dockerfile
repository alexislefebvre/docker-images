FROM jakzal/phpqa:php7.4-alpine

RUN apk add --no-cache libpng-dev \
 && docker-php-ext-install -j$(nproc) iconv \
 && docker-php-ext-configure gd \
 && docker-php-ext-install -j$(nproc) gd
