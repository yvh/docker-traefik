# docker-traefik



## Requirements

- docker
- docker-compose plugin

## Setup

Create a docker network

```bash
docker network create traefik
```

Run traefik container

```bash
docker compose up -d
```

## Template of docker compose for project

```yaml
services:
    nginx:
        image: nginx
        labels:
            - traefik.enable=true
            # change port
            #- traefik.http.services.<project-name>.loadbalancer.server.port=8080
            - traefik.http.routers.<project-name>.entrypoints=http
            - traefik.http.routers.<project-name>.rule=Host(`example.localhost`)
            # redirect-to-https
            #- traefik.http.routers.<project-name>.middlewares=redirect-to-https@file
            # configure https
            #- traefik.http.routers.<project-name>_secure.entrypoints=https
            #- traefik.http.routers.<project-name>_secure.rule=Host(`example.localhost`)
            #- traefik.http.routers.<project-name>_secure.tls=true
        volumes:
            - ./html:/usr/share/nginx/html
        networks:
            - traefik

networks:
    traefik:
        external: true
```
