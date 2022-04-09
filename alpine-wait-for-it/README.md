# wait-for-it.sh

[wait-for-it.sh](https://github.com/vishnubob/wait-for-it) in a image

Use this image with Drone by using this `.drone.yml`:

```yml
pipeline:
  wait-for-it:
    image: ghcr.io/alexislefebvre/alpine-wait-for-it
    commands:
      - mysql:3306 --timeout=60
```
