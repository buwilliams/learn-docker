# Tiny PostHog

The goal of this project is to (1) have a tiny docker environment for localdev that works on Apple M1 and (2) learn Docker in the process

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