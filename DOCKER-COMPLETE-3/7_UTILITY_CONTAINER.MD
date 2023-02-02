# Utility container

1. Why would you use them?
???
docker exec -it abc npm init

**CMD vs ENTRYPOINT in Dockerfile**
 CMD : be overrided by command which was injected in docker running
 ENTRYPOINT: append


So you can add a utility containers as save time to write command by useing ENTRYPOINT in utility containers

**Some time you can use the docker-compose without Dockerfile when you don't need dockerfile any way E.g: build utility for node**

### bind mount with volume and COPY - Which should be chosen

Use copy if you don't need the real update'

WORKINGDIR in docker file as the cd function :D
