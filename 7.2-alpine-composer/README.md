# PHP 7.2 from Alpine Linux with Composer

Use this image with Drone by using this `.drone.yml`:

```yml
pipeline:
  test:
    image: ghcr.io/alexislefebvre/7.2-alpine-composer
    volumes:
      - composer-cache:/root/.composer
    commands:
      - composer install -vv --profile --no-progress
      - php vendor/bin/phpunit
    environment:
      - SYMFONY_ENV=test
```
