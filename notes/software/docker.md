# Docker

- **OCI** - Open Container Initiative
    - image and runtime specification
    - implemented by Docker, rkt, not sure about LCX
- process vs. container vs. VM
    - process - poor isolation
    - VM - too heavy
- each container
    - has isolated network interface
    - shares the kernel with the host
    - shares the same file system layers with all containers
- rules of thumb
    - **one process per container**
    - **order your `Dockerfile` commands to optimize caching** (what changes goes last)
- build context - can be reduced with `.dockerignore`
- if a service can **run without privileges**, use `USER` to change to a non-root user
- **Jib** (by Google) - builds optimized Docker and OCI images for your Java applications without a Docker daemon

## Sources

- [Docker Cache – How to Do a Clean Image Rebuild and Clear Docker's Cache](https://www.freecodecamp.org/news/docker-cache-tutorial/) (
  freeCodeCamp blog)
- [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Building on solid ground: reproducible Docker builds for Python](https://pythonspeed.com/articles/reproducible-docker-builds-python/)
- [Building Docker Images - Best Practices](https://youtu.be/JcGwgNMZc_E?si=RdF_c16NkRcxRgRc)

## Build cache

- `--no-cache` to run a clean build
- `FROM` - cached, SHA is validated against repository
- `ADD`, `COPY` - cached, SHA is validated
- `RUN` - cached, key is the exact command (string)
    - cache busting - uses exact versions, changing a version busts the cache
    - always run `apt-get update && apt-get ...` in a single command, otherwise `apt-get update` is skipped
- if an upper directive is not in cache, then all the following commands are not taken from cache either
    - i.e. a new version of Docker base image (`foo:latest` with new SHA) will run `apt-get ...`
    - i.e. order of commands matter - things that change often goes last, so we don't rebuild everything
- each command is a separate layer, layers are additive so deleting something in a different command (layer) has no effect

## Multi-stage builds

- separate stages for the application build (might require tooling like compilers and create temporary files)
- only the last stage is preserved, usually just copies the final build from previous stages
- shrinks total size and eliminate potentially dangers tools

## Reproducible builds

- version pinning
    - base image
    - system packages
    - app dependencies
- extreme approach - `python@sha256:89d719142de465e7c80195dff820a0bbbbba49b148fbd97abf4b58889372b5e3`

## Pruning

- docker can eat up lots of space in `/var/lib/docker`
- `docker IMAGE/CONTAINER/VOLUME prune -a`