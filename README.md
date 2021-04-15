# Tiny PostHog

The goal of this project is to (1) have a tiny docker environment for localdev that works on Apple M1 and (2) learn Docker in the process

## Docker Nomenclature and Notes

- `Docker Image` - the actual package, **artifact** which can be shared with others
- `Docker Container` - a *running* instance of a docker image, file system is virtual, contains a port for communication
- Docker run - only fetches the layers of a image it doesn't already have locally
- Docker vs Virtual Machine
    - Operating System = Hardware > OS Kernel (layer 1) > Applications (layer 2)
    - Docker = Virtualization of applications (layer 2)
    - Virtual Image = Virtualization of OS (layer 1)
    - Benefits of Docker = images are much smaller, runs faster
    - Benefits of VM = you can run different OS (Windows on Linux) since it has it's own OS Kernel
- Docker Port vs Host Port
    - Multiple containers may use the same port
    - Bind host port to docker port, i.e. host 3000 -> docker 3000, host 3001 -> docker 3000

## Basic commands

- `docker pull` downloads a docker image locally
- `docker images` shows a list of local docker images and their sizes
- `docker run` run a docker container, it's two commands in one *docker pull* and *docker start*
- `docker run -d` runs the docker container in *detach mode*
- `docker run -p` binds the container to host port i.e. *-p6000:6370*, *-p[host]:[container]*
- `docker start` start a container
- `docker stop` - stops a container
- `docker ps` shows *running* containers
- `docker ps -a` shows *running and not-running* containers
- `docker exec -it`
- `docker logs`

## First Dockerfile

```docker
FROM python:3.9-alpine3.13

RUN apk add bash nodejs

COPY hello.* /

CMD ["bash"]
```

## First commands

 - `docker build .` builds the container
 - `docker run --name [name] [sha]` installs the container
 - `docker run -it --name [name] [sha]` installs the container and starts in interactive mode
 - `docker ps` shows all the running containers
 - `docker ps -a` shows all the running and exited containers
 - `docker stop [name]` stop container
 - `docker start -ai [name]` start container interactively
 - `docker rm [name]` removes container

## Getting started

- `git clone https://github.com/buwilliams/tiny-posthog.git`
- `cd tiny-posthog`
- `docker build .`
- `docker run -it --name test [sha]` find sha in the output from docker build

 ## Resources

 - [Creating your first Dockerfile, image and container](https://www.youtube.com/watch?v=hnxI-K10auY)
 - [Docker For Beginners: From Docker Desktop to Deployment](https://www.youtube.com/watch?v=i7ABlHngi1Q)
 - [Docker Tutorial for Beginners [FULL COURSE in 3 Hours]](https://www.youtube.com/watch?v=3c-iBn73dDE)