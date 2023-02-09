# Building Muti-containers

### Module content

### Create a network for this group application
 > docker network create goals
 Then you can create all your containers in by this network that mean all application are running in the same network.
 > docker run --name mongodb --rm -d --network goals mongo
 > docker run --name goals-fe -p 3000:3000 --rm -d --network goals goals-fe:latest
 > docker run --name goals-be -p 80:80 --rm -d --network goals goals-be:latest
 Our FE is react fe and it's running in browser so It can't access to BE by container even all of them in the same docker network -> we have to expose port 80 to outside then fe can connect to be by port 80

### Add Data persistent to MongoDB with Volumnes
 As you see when remove the mongoDB then rerun the mongoDB we lost the old data so we need to do it to keep the data so we have to run mongo with volumne
 Goals are data should be persist and access should be limited
 > docker run --name mongodb -v data:/data/db -rm -d --network goals mongo
 In the case you would like to send the variables to run containers then you can add this command to your docker running command.
 > -e username=thanh -e password=secret
 If you add user name and password for mongodb you have to change in the source code to connect mongodb by new link with username password
 
 ### Volumes, Bind Mounts & Polishing for the NodeJS BACK ENd Containers.
 Data must persist and live source code update
 > docker run --name goals-be -v logs:/app/logs -v ${your local machine link source code}:/app -v /app/node_modules -e MONGODB_USERNAME=thanh -e MONGODB_PASSWORD=secret -d --rm -p 80:80 --network goals goals-be:latest

### Live source code update for FE container
 > docker run -v ....src:/app/src --name goals-fe -p 3000:3000 --rm -d --network goals goals-fe:latest
 Same as BE you can map the folder which have source code in your host machine to container.

### Reload source code for window wsl 2 for docker
 Read window [./windows-wsl2-file-events.pdf]

### Have to Improve
 1. The long command alway repeat all time when stop and start, long docker run command. Would be great, if we wouldn't have to remember/save those and if wouldn't have run them individually

 2. Depvelopment only setup -> Not optimized for production shouldn't executed like this on a production server