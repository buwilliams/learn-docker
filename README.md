# Learning Docker

The goal of this project is to have a tiny docker environment for localdev that works on Apple M1.

## First Dockerfile

```docker
FROM python:3.9-alpine3.13

RUN apk add bash nodejs

COPY hello.* /

CMD ["bash"]
```

## First commands

 - `docker build .` - builds the container
 - `docker run --name [name] [sha]` - installs the container
 - `docker run -it --name [name] [sha]` - installs the container and starts in interactive mode
 - `docker ps`
 - `docker stop [name]`
 - `docker start -ai [name]`
 - `docker rm [name]`

 ## Resources

 - [Creating your first Dockerfile, image and container](https://www.youtube.com/watch?v=hnxI-K10auY)
 - [Docker For Beginners: From Docker Desktop to Deployment](https://www.youtube.com/watch?v=i7ABlHngi1Q)