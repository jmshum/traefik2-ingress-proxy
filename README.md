# Traefik 2 proxy/dashboard and load balancer for Docker Swarm or Docker Compose
These are two example configurations for an ingress service using [Traefik 2](https://containo.us/traefik/) as a reverse proxy / load balancer for [Docker Swarm](https://docs.docker.com/engine/swarm/) and [Docker Compose](https://docs.docker.com/compose/). This will allow each container to be published on the same port (e.g. port 80, 443), but hosting multiple web domains. This also includes a traefik dashboard and a Docker Swarm dashboard.

# Documentation
[Traefik 2 documentation](https://docs.traefik.io/v2.1/providers/docker/#docker-swarm-mode)

[Docker Swarm](https://docs.docker.com/engine/swarm/)

[Docker Compose](https://docs.docker.com/compose/)

## Usage
Choose either the Docker Swarm (swarm-traefik.yml) or the Docker Compose (docker-compose.yml) implementation. This will create containers for an [nginx](https://hub.docker.com/_/nginx) web server (example2.com) and a tiny [Go webserver](https://hub.docker.com/r/containous/whoami/dockerfile) (example.com). Both being published on port 80. It will also create a [Traefik 2](https://hub.docker.com/_/traefik) container to handle ingress traffic through reverse proxy and load balancing. There is also a container that will be created in the Swarm configuration for a [visualizer dashboard](https://hub.docker.com/r/dockersamples/visualizer) (Swarm only). 

### Docker Swarm
* Add ```127.0.0.1 example.com``` to your /etc/hosts file
* Add ```127.0.0.1 example2.com``` to your /etc/hosts file
* example.com:8080 for traefik dashboard
* example.com for whoami website
* example2.com for nginx website
* Docker Swarm visualizer runs on port 5000

Running in a Swarm service
```bash
docker stack deploy -c swarm-traefik.yml example-stack
```

### Docker Compose
* Add ```127.0.0.1 example.com``` to your /etc/hosts file
* example.com:8080 for traefix dashboard
* example.com for whoami website

Running with docker-compose
```bash
docker-compose up
```
or scale your webpage containers
```bash
docker-compose up -d --scale webpage=2
```