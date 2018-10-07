# docker-images

Use this image with Drone by using this `.drone.yml`:

```yml
pipeline:
  test:
    image: alexislefebvre/docker-images:7.2-alpine-composer
    commands:
      - composer install -vv --profile --no-progress
      - php vendor/bin/phpunit
```  
