# Networking in docker for container communication 
  1. Case 1: Container to WWW Communication
    We would like to get data from a outside link www E.g: https://swapi.dev/api/films
    No special config, it can work with www
  2. Case 2: Contaienr to your host machine communication
    You have use host.docker.internal instead of localhost address
    E.g: localhost:4500 -> host.docker.internal:4500
  3. Case 3: Container to other containers comunication
    This is common case and best pactice
     Using ip of container (to get ip of container we can use inpsect) but container started
    
## Creating Container Networks
  > docker network create favorites-network
  > docker run -d --name mongodb --network favorites-network mongo

  To connect to this container can use 'mongodb://mongdb:27017/'
  All cotainers should have same network.
  You don't need the public the port to outside by -p in docker run if you don't need to access it from your host machine.

## Docker network drivers
 ***Default driver is bridge*** make the most sense in the vast majority of scenarios
 **bridge** : container can find each other by name if they are same the network.
 **host** : Isolation between container and host system is removed (they share local as a network) //todo read more about that
 **overlay**: Multiple docker daemon (docker running in different machines) are able to connect with each other. Only works in "Swarn" mode which is a dated/almost deprecated way of connecting multiple containers. --- don't use it
 **macvalan** You can set a custom MAC address to a container - this addresscan be used for communication with that container.
 **none** all network is disabled
 **third-party plugin** You can install thrid party plugins which then may add all kinds of behaviors and functionalitites.

