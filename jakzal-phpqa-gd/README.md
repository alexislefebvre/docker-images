# jakzal/pqpqa with GD

Use this image with Drone by using this `.drone.yml`:

```yml
pipeline:
  phpstan:
    image: alexislefebvre/docker-images:jakzal-phpqa-gd
    group: tests
    commands:
      - phpstan analyse --level 6 src/ --no-progress
```
