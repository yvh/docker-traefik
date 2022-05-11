# docker-traefik



## Requirements

- docker
- docker-compose

## Setup

Create a docker network

```
docker network create traefik
```

Run traefik container

```
docker-compose up -d
```

## Template of docker-compose for project

```
version: '3.8'

services:
    nginx:
        image: nginx
        labels:
            - traefik.enable=true
            - traefik.http.routers.project-name.rule=Host(`project-name.local`)
            - traefik.http.routers.project-name.entrypoints=insecure
        volumes:
            - ./html:/usr/share/nginx/html
        networks:
            - traefik

networks:
    traefik:
        external: true
```
