# Apache

[![This image on DockerHub](https://img.shields.io/docker/pulls/stefanscherer/apache-windows.svg)](https://hub.docker.com/r/stefanscherer/apache-windows/)

Open JDK in a Windows NanoServer container.

## Build the image

```
docker build -t openjdk:1.8.0-nanoserver-1809 .
```

## Run the container

```
docker run -d openjdk:1.8.0-nanoserver-1809
```