# PHP 8.1 from Alpine Linux with Composer and GD

Use this image with Drone by using this `.drone.yml`:

```yml
pipeline:
  test:
    image: ghcr.io/alexislefebvre/php-8.2-alpine-composer-gd
    volumes:
      - composer-cache:/root/.composer
    commands:
      - composer install -vv --profile --no-progress
      - php vendor/bin/phpunit
```
