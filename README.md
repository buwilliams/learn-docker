# Learn Docker via PostHog

The goal of this project is to (1) have a tiny docker environment for localdev that works on Apple M1 and (2) learn Docker in the process. You can read the progress of this repo in the [project doc](PROJECT.md).

## Docker Nomenclature and Notes

- `Docker Image` - the actual package, **artifact** which can be shared with others, docker images are built in layers via Dockerfile
- `Docker Container` - a *running* instance of a docker image, file system is virtual, contains a port for communication
- Docker run - command which executes *pull* and *start* (only pulls images we do not have locally)
- Docker vs Virtual Machine
    - Operating System = Hardware > OS Kernel (layer 1) > Applications (layer 2)
    - Docker = Virtualization of applications (layer 2)
    - Virtual Image = Virtualization of OS (layer 1)
    - Benefits of Docker = images are much smaller, runs faster
    - Benefits of VM = you can run different OS (Windows on Linux) since it has it's own OS Kernel
- Docker Port vs Host Port
    - Multiple containers may use the same port
    - Bind host port to docker port, i.e. host 3000 -> docker 3000, host 3001 -> docker 3000
- `Docker Compose`
    - Configuration file specifying *docker commands* to make it easier to work with
    - Automatically handles creating a common *docker network*
    - Docker compose is usually installed with docker so you already have it
- `Docker Volumes`
    - Provides data persistence between host machine and docker containers
    - The data between volumes is replicated between the host and docker container volumes
    - 3 docker volume types: specified, anonymous, and named volumes, named volumes on the host are managed by docker
    - Production should use *named volumes*
    - Container Mongodb = /data/db
    - Container MySQL = /var/lib/myself
    - Container Postgres = /var/lib/postgres/data
    - Host Windows = C:\ProgramData\docker\volumes
    - Host Linux = /var/lib/docker/volumes/[hash]/_data
    - Host Mac = /var/lib/docker/volumes/[hash]/_data
        - `screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty` add access linux VM on mac where data is stored, `ctrl + a + k` to exit screen session

## Basic commands

- `docker pull` downloads a docker image locally
- `docker images` shows a list of local docker images and their sizes
- `docker run` run a docker container, it's two commands in one *docker pull* and *docker start*
- `docker run -d` runs the docker container in *detach mode*
- `docker run -p` binds the container to host port i.e. *-p6000:6370*, *-p [host]:[container]*
- `docker run --name` give the container a name so that you do not need to use the SHA
- `docker run -d -it python` runs python images in *interactive terminal* mode
- `docker run -e` runs an image with an environment variable
- `docker run -net` specify a docker network to run within
- `docker start` start a container, retains the settings from the run command
- `docker stop` - stops a container
- `docker ps` shows *running* containers
- `docker ps -a` shows *running and not-running* containers
- `docker logs` shows the *standard output* of the *running* container
- `docker logs -f` follow the *standard output*, similar to *tail -f*
- `docker exec -it` runs the container with interactive terminal
- `docker network ls` shows a list of the internal docker network
- `docker network create` create a docker network
- `docker build -t my-app:1.0 .` builds an image from a *Dockerfile* in the current directory
- `docker rm` removes a docker container which you need to do before docker rmi
- `docker rmi` removes a docker image, i.e. docker rmi my-app:1.0
- `docker run -v` mounts host filesystem to docker container filesystem
- `docker system prune` clean up any images, containers, volumes, and networks that are dangling
- `docker system prune -a` any stopped containers and all unused images

## Docker Compose

- `docker-compose -f mongo.yaml up` pulls, starts, and creates container network
- `docker-compose -f mongo.yaml up -d` runs containers in *detached mode*
- `docker-compose -f mongo.yaml down` stops container, removes container, and stops container network

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

 - [Creating your first Dockerfile, image and container](https://www.youtube.com/watch?v=hnxI-K10auY) great place to start
 - [Docker Tutorial for Beginners [FULL COURSE in 3 Hours]](https://www.youtube.com/watch?v=3c-iBn73dDE) most helpful
 - [Docker For Beginners: From Docker Desktop to Deployment](https://www.youtube.com/watch?v=i7ABlHngi1Q)

 ## Related Resources

 - [Kubernetes Tutorial for Beginners FULL COURSE in 4 Hours](https://www.youtube.com/watch?v=X48VuDVv0do) To manage distribution of contains across many servers

 ## Ideas

 - It's possible to run only the containers that are needed for PostHog's EE
 - [Build Clickhouse for ARM64](https://clickhouse.tech/docs/en/development/build-cross-arm/)
 - Is it possible to docker-compose conditionally based on architecture? If so, I think we have a solution for PostHog EE on Macbook Silicon/M1.
    - This [Stack Overflow question](https://stackoverflow.com/questions/50387076/docker-compose-conditional-statements-e-g-add-volume-only-if-condition) may contain the answer. Solution: generate docker compose files
