# Assignment 4 - Docker & Containerization


##  1. Introduction to Containerization and Docker Fundamentals, Basic Commands

###  Commands Used
```bash
docker --version
docker run hello-world
docker ps -a
docker images
docker stop 7363d0cc10c5e2b6a5f35ed49e424255f007ae599a942c2d49f6aebb99090dd8
docker rm 7363d0cc10c5e2b6a5f35ed49e424255f007ae599a942c2d49f6aebb99090dd8
docker rmi 7363d0cc10c5e2b6a5f35ed49e424255f007ae599a942c2d49f6aebb99090dd8
```
Outcome: Learned Docker's role, container lifecycle, and difference from virtual machines.

 2. Docker Installation and Basic Container Operations, Build an Image from Dockerfile
Installed Docker and explored basic container operations. Built a custom image using a simple Dockerfile.

 Dockerfile
dockerfile
```
FROM alpine
CMD ["echo", "Hello from Docker!"]
```
Commands Used
```
docker build -t hello-docker .
docker run hello-docker
docker run -it --name alpine-test alpine
docker exec -it alpine-test sh
```
 Outcome: Understood image creation, container launch, and command-line interaction with containers.

3. Docker Registry, DockerHub, Multi-Stage Build
Created a DockerHub account and pushed images. 

Commands Used
```
docker login
docker tag hello-docker suhanisingh/hello-docker
docker push suhanisingh/hello-docker
docker pull suhanisingh/hello-docker
```
Multi-Stage Dockerfile Example
dockerfile
```
FROM golang:alpine as builder
WORKDIR /app
COPY . .
RUN go build -o app

FROM alpine
COPY --from=builder /app/app /app
ENTRYPOINT ["/app"]
```
Outcome: Learned image versioning, publishing, and best practices for smaller and secure builds.

4. Create a Docker Image Using Multiple Methods
Built Docker images using:

Dockerfile

Existing running containers

Commands Used
```
docker run -it alpine
# Made file changes inside
docker commit 7363d0cc10c5e2b6a5f35ed49e424255f007ae599a942c2d49f6aebb99090dd8 custom-alpine
```
Outcome: Learned different approaches to create custom images.

5. Push and Pull Image to DockerHub and Azure Container Registry (ACR)
Practiced pushing images to DockerHub and Azure ACR.

Commands Used
```
# DockerHub
docker login
docker push suhanisingh/hello-docker
```
```
# ACR
az login
az acr login --name myregistry
docker tag hello-docker myregistry.azurecr.io/hello-docker
docker push myregistry.azurecr.io/hello-docker
```
Outcome: Understood public/private container registries and CI/CD integration.

6. Create a Custom Docker Bridge Network
Created a custom bridge network and enabled communication between containers.

 Commands Used
```
docker network create my-bridge
docker run -dit --name c1 --network my-bridge alpine
docker run -dit --name c2 --network my-bridge alpine
docker exec -it c1 ping c2
```
Outcome: Learned container networking and isolation.

7. Create a Docker Volume and Mount it to a Container
Explored persistent storage using Docker volumes.

Commands Used
```
docker volume create my-vol
docker run -dit --name voltest -v my-vol:/data alpine
docker exec -it voltest sh
echo "Persistent" > /data/file.txt
```
Outcome: Understood how to retain data across container restarts.

8. Docker Compose for Multi-Container Applications & Security Best Practices
Used Docker Compose to manage multiple services and followed security best practices.

docker-compose.yml
```
version: "3"
services:
  nginx:
    image: nginx
    ports:
      - "8080:80"
  redis:
    image: redis
```
Commands Used
```
docker-compose up
docker-compose down
```
