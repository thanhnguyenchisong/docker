# Build  the image and tun a container
 FROM, WORKDIR, COPY, RUN will run at image building time => It create a image template but we don't run it as application
 So the start application command don't used RUN => use CMD => It will run at container running based on this image.

**Docker container is isolated with our side** => we have to expose to local machine by port.

After finish the DOCKER file.
- Build docker image
 > docker build . -t nodeapp:v1
<!-- docker image ls to check the image in our local -->
- Docker run
 > docker run -p 3000:80 nodeapp:v1
<!-- docker ps to check running containers -->


### The image is read only if would like to change the source you have to build a new image

**[Small optimization] Building docker image, every instruction in an image creates a cacheable layer which can help with image rebuild and sharing so if you don't change anything and rebuild the image, it use the data from cache so it is fast for rebuilding with no change**

 But when you change a data impact directly to a step, all of next steps/layer don't use the cache and do the real rebuild.

 For our Dockerfile. we have COPY package.json to /app first because we don't alaways change the libs in package.json, most of the change from source code on app. So step from head to RUN npm install will reload from cache so it can save time.

### Managing Images & Containers.
 Can you docker --help to see all options
 1. Image
 docker -t
 docker images
 docker image inspect
 docker rmi
 docker prune
 2. Container
 docker rm 
 docker ps
 docker ps -a
 docker start
 docker stop, ...

### Attached & Detached containers
 - Attached mode is default when init a instance running with docker run => so you can't interact with terminal more but see the logs inside containers.
 - Detached mode is -d <sup> docker logs -f --tail 1 CONTAINER </sup>

 > docker attach CONTAINER
It will run the docker attach mode.

### Entering interact mode
- Some application interact directly to you in console as input value but docker don't provide it as default
-i : you can input something to container.
-t : create a terminal
So combite -it we can interact with container with current terminal 
**Example** input a value for some specific logic applications - input 10, 5 in termial and do the comparision or long running process after input

### Remove
docker rmi IMAGE   => remove a specific image.
docker image prune => remove unused image
docker --rm run .... => auto remove the container after stop
docker rm CONTAINER
### Inspect a image & importain information
 > docker image inspect IMAGE
- Id : id of image.
- ExposePorts : ports can be used
- ENTRYPOINT: default command to run when start container
- Docker version
- Os

### Copy content vm and containers.
> docker cp : to copy something to in/out contaiers.

### Naming & Tagging Containers and Images
--name : option to set container name
-t/--tag : format name:tag to set the name and version of image

### Sharing images & containers
- Share Dockerfile
- Shere a Built Image - push image to docker hub or private registry

### Push/pull to docker hub
> docker push IMAGE_NAME
> docker pull IMAGE_NAME

To push correct registy the name of image should be 
> {registry}/IMAGE_NAME:version
if it is not correct name, we can use the cmd: 
> docker tag IMAGE_NAME:version 
> {registry}/IMAGE_NAME:version 
to clone to the new name.
After that we can push correct image to registry by 
> docker push {registry}/IMAGE_NAME:version 
Note: Have login with **docker login link**