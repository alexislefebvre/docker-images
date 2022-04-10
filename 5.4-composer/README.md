# PHP 5.4 with Composer

Use this image with Drone by using this `.drone.yml`:

```yml
pipeline:
  test:
    image: ghcr.io/alexislefebvre/5.4-composer
    volumes:
      - composer-cache:/root/.composer
    commands:
      - composer install -vv --profile --no-progress
      - php vendor/bin/phpunit
    environment:
      - SYMFONY_ENV=test
```

If you have this error when running Composer:
 
```bash
Fatal error: Allowed memory size of 1610612736 bytes exhausted (tried to allocate 32 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleSetGenerator.php on line 126`:
```

Set the `memory_limit` to `-1` to disable the limit:

```bash
docker run -it --volume $PWD:/app --workdir /app alexislefebvre/docker-images:5.4-composer php --define memory_limit=-1 /usr/local/bin/composer update -vvv
```
