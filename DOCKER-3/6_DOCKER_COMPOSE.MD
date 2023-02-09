# DOCKER COMPOSE

### What is docker compose
The tool alows you do multiple docker build and run command with a main command
We have a configruation file which can share anyone and then it's just one command - no command copy and pasting, a command leverage this configuration file
 1. What Docker Compose is NOT
  - Docker compose does not replace Dockerfiles for custom Images.
  - Docker Compose doesn't replace Images or Containers.

  **It just make luching containers ways easier with saving extra command**
  - Docker Compose is NOT suited for managing multiple containers in different host.

### Writing Docker Compose files.
1. Create docker-compose.yaml file
2. Use command
 > docker-compose up -d
 Start with detach mode
 > docker-compose down
 Delete all containers, default network, not for volumes, if you also would like to delete volume, have to add option -v as command below
 > docker compose down -v

 > docker compose up --build
 Force to rebuild the images.
 > docker compose buid
 Build any missing image and then not start containers, just build images.

 **Service name can be used as hostname for connect bw services**

 ***NOTE***
 The name of containers is not the service name in docker compose

  