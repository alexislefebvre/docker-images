# PHP 7.4 from Alpine Linux with Composer and GD

Use this image with Drone by using this `.drone.yml`:

```yml
pipeline:
  test:
    image: ghcr.io/alexislefebvre/php-7.4-alpine-composer-gd
    volumes:
      - composer-cache:/root/.composer
    commands:
      - composer install -vv --profile --no-progress
      - php vendor/bin/phpunit
```
