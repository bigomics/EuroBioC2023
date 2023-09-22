include settings.env
##export $(shell sed 's/=.*//' settings.env)

deploy: 
	docker stack deploy -c traefik.yml traefik
	docker stack deploy -c app.yml app

rm:
	-docker stack rm app
	-docker stack rm traefik

ls:
	watch docker service ls

init:
	docker swarm init ## --advertise-addr 192.168.1.222
	docker network create --driver=overlay traefik-public
	docker node update --label-add traefik-public.traefik-public-certificates=true ${MANAGER_NODE}

destroy: rm
	-docker swarm leave --force
	-docker volume rm traefik_traefik-public-certificates
	-docker network rm traefik-public
