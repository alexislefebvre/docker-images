# PHP 7.1 from Alpine Linux with Composer and GD

Use this image with Drone by using this `.drone.yml`:

```yml
pipeline:
  test:
    image: ghcr.io/alexislefebvre/7.1-alpine-composer-gd
    volumes:
      - composer-cache:/root/.composer
    commands:
      - composer install -vv --profile --no-progress
      - php vendor/bin/phpunit
    environment:
      - SYMFONY_ENV=test

services:
  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: project
      MYSQL_USER: user
      MYSQL_PASSWORD: userpass
```
