# jakzal/pqpqa on PHP 8.2 with GD

Use this image with Drone by using this `.drone.yml`:

```yml
pipeline:
  phpstan:
    image: ghcr.io/alexislefebvre/php-8.2-jakzal-phpqa-gd
    group: tests
    commands:
      - phpstan analyse --level 6 src/ --no-progress
```
