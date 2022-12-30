# Managing Data & Working with Volumns

### Data
Application (Code + Environment) - read only hence stored in Images
Temporary App Data (e.g entered user input) - Read + write hence stored in Containers.
Performance App Data(e.g user accounts) - Read + write stored in container and volumns

### Volumes
    FA folder/file inside of Docker container which is connected to seome folder outside of the container
    Volumes persist if a container shut down. Container can read and write to volume
    Situation: After remnove the container -> the data also be remove if you don't store it in ourside of containers. -> we have volunmes.

### Tow type of Extenral Data Storeages
1. Voulumes (Managed by Docker)
 Docker sets up a folder / path on your host machine exact location is unknown to you
 Managed via docker volumne commands.
 **Impotaint: It is not managed by you, can't edit directly, don't know where is stored folder in host machine**
 -  Anonymous Volumes - Have generated name - rm container -> volume be removed
   You can create Anonymous Volumes by set volumne in docker image by VOLUME tag or wihout container name with -v option in docker running container
 -  Named Volumes - name by you - Remove container -> volume is still existed
   You can create Named Volumes by assigning name of volume to container folder in running container command. 
   E.g: 
   > docker run -d -p 3000:80 --rm --name feedback-app -v feedback-volume:/app/feedback  feedback-node:v1
   -v option is volume, feedback-volume is volume name and /app/feedback is folder in cotainer.
2. Bind Mounts (Managed by you)
 That mean you can change the volume content directly.
 E.g: 
 > docker run -d -p 3000:80 --rm --name feedback-app -v feedback-volume:/app/feedback -v /mnt/d/tech/docker/DOCKER-COMPLETE:/app -v /app/node_modules  feedback-node:v1
 
 We add a mount from your host folder to a container folder so the docker will never override the file having same name from container to your host - It is a good point. We have 1 more mount  -v /app/node_modules. Which have container link loger will override others. So after run -v /mnt/d/tech/docker/DOCKER-COMPLETE:/app then we don't have node_modules in your host so we force container - The node_modules can be created by you conatainer. So the npm install run command will work fine.

 ** Benefit - when we change the code in host machine - the container content also change immedialy  for coding which run running time **
 You can retric the permistion read only by add ${pwd}:/app:ro

 ##### COPY in Dockerfile
 - We have a .dockerignore file stay in same folder with Dockerfile to ignore file.

 ##### Working with Environment Variable & .env file
  1. Agguments & environment variable
     - Agguments available inside of Dockerfile, not access by CMD or any application code and setted on image build **docker build** via **--build-arg**
       Put ARG keyword in  your Dockerfile and you can use command
       > docker build -t feedback-note:v1 --build-arg DEFAULT_PORT=8000 .
     - EVN variable available inside of Dokerfile & in application code, setted via ENV in Dockerfile ỏ via **--env or -e on docker run**
       E.g: 
       > docker run -d -e PORT=8000 -p 3000:8000 --rm --name feedback-app -v feedback-volume:/app/feedback -v /mnt/d/tech/docker/DOCKER-COMPLETE:/app -v /app/node_modules  feedback-node:v1
       In the case you had config .evn file you can use  **--env-file ./.env** to use the variable which was declared in **.env** file
       > docker run -d --env-file ./.env -p 3000:8000 --rm --name feedback-app -v feedback-volume:/app/feedback -v /mnt/d/tech/docker/DOCKER-COMPLETE:/app -v /app/node_modules  feedback-node:v1
  ** The sensitive data shouldn't stored in Dockerfile because after building it can be read by docker history IMAGE. So we should send it on docker run or in sepate file and make sure don't commit it **
  







