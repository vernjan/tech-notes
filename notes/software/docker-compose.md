# Docker Compose

## Networking
- see https://docs.docker.com/compose/networking/
- `HOST_PORT:CONTAINER_PORT`
- containers on the same network: `service name + CONTAINER_PORT`
- host to container: `localhost/DOCKER_IP + HOST_PORT`
- container to host: `host.docker.internal`