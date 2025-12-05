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

Use with image in `Makefile` to wait for the database:

```makefile
install: ## Install
	docker run ghcr.io/alexislefebvre/alpine-wait-for-it 172.17.0.1:3306 --timeout=30
	docker compose exec php sh -c "composer install --no-interaction"
	docker compose exec php sh -c "bin/console --env=test doctrine:database:drop --if-exists --force"
	docker compose exec php sh -c "bin/console --env=test doctrine:database:create --if-not-exists"
	# …
```

Source of the script: https://github.com/vishnubob/wait-for-it/blob/81b1373f17855a4dc21156cfe1694c31d7d1792e/wait-for-it.sh
