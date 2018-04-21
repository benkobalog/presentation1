# Docker

![docker](https://techglimpse.com/wp-content/uploads/2016/03/Container-vs-VMs.jpg)

## Basic concepts
* Container
* Image
* Dockerfile
* Volume
* Registry

#### Container
* A container is an instance of an image that can start, pause, stop
```bash
docker run --name <container name> <image name>
# If --name is omitted the container will get a generated name
docker stop <container name>
docker start <container name> # start stopped container (or one that has just been created)
docker rm <container name> # deletes content
docker logs <container name> # inspect stdout and stderr
docker exec -it <container name> bash # if bash is installed in the container you can launch a shell inside it
```
* Uses the same kernel as the host OS, but you can run any linux distro, regardless of the host OS
* Processes inside the container are separate from the host

#### Image
* Images are read-only definitions used to create a container (they describe the content of a container, starting with a base image, at the very least a base Linux OS)
* Images can be used as the starting point and extended to create other images
* Images are layered
    * Images stored on the machines can share layers, which can save disk space
    * Layers are not rebuild unless you add "--no-cache" to the build command

```bash
docker build -t <image name> .
docker rmi <image name>
```

#### Dockerfile

```docker
FROM openjdk:8-jre

COPY /target/scala-2.12/testwebapi-assembly-0.0.1-SNAPSHOT.jar /root/app.jar

RUN echo "you can run commands here which run during the build phase"

ENTRYPOINT java -Xms100m -Xmx100m -jar /root/app.jar
```
* Images are built from Dockerfiles
* Each command ('RUN', 'COPY', etc.) represents a layer

#### Registry
* "Repo" for images
* Images on https://hub.docker.com/explore/ is available by default on all docker clients
* You can also use other docker registries
* AWS provides ECR for this purpose
```bash
 docker pull <image name>
 docker push <image name> 
```

#### Volumes
* "Folders" which can be attached to containers
* Use -v switch on "docker run" to attach containers
* Data on volumes is not deleted when a container is deleted

## Data

* Data created after a container has been launched will be lost if the container is deleted
* Persisted data should be stored elsewhere - DB, S3, volumes etc.
* Containers should be 
"stateless"
* "Starting data" is not visible from the host OS. (But you can copy it with _docker cp_)

## Network

* Outgoing traffic has the same limitations as the host machine
* Incoming traffic is closed by default
    * all ports are closed
    * ports can be opened with -p switch
* Containers can have separate IP addresses
