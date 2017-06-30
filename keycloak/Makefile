# Environment Variables
CONTAINER = authorization_server

.PHONY: up

prep :
	mkdir -p \
		data/postgres \
		data/keycloak

pull :
	docker-compose pull

up : prep # pull
	docker-compose up -d

stop :
	docker-compose stop

down : stop
	docker-compose rm -f

shell :
	docker exec -ti $(CONTAINER) /bin/bash

tail :
	docker-compose logs -f --tail 200
