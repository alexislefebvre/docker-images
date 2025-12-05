# PHP 8.3 from Alpine Linux with Composer

Use this image: `ghcr.io/alexislefebvre/php-8.3-alpine-composer`

Example with Docker Compose for a Symfony project:

```yaml
services:
    php:
        image: ghcr.io/alexislefebvre/php-8.3-alpine-composer
        working_dir: /app
        ports:
            - 8000:8000
        volumes:
            - ./:/app/
        entrypoint: php --server 0.0.0.0:8000 --docroot public/
```
