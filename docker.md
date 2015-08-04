


coreos, mesos -linux distros  OS where multiple computers acts as one
computer and they share resources as one comupter. When you run ouf of
resources you can add more machines to cluster => will increase cluster
memory / processor power. This is ideal for docker as it's container is
using only required amounts of memory /processor power.

- docker client (user interface)
- docker daemon (sits on the server )
- docker index == docker repository of docker images (docker hub)
- docker container = actual container running the application includes
  filesystem, ports, processes space isolated from  host
- docker image == equivalent of VM , snapshot of running container, can
  be version controled => `docker diff` => you can check changes and
then push to dockerhub
- docker file =  similar to cheff file, holds instructions how to build
  container
- docker layer = ??? is stacked each time docker mounts root fs ???
-


in theory a single docker container should run only one process (ruby
container, postgres container) . When this main process dies docker
container will go down (equivalent of `docker kill`)  (ref: [1]#27:00)
... sometimes you want to run multiple processes in onne container
(early development) check supervisor


docker commands 

-  docker run <image>   # creates and run a docker container
- docker pull <image> # pull prebuild image from repo (dockerhub)
- docker commit  # save container state as image (equivalent to a layer)
- docker images # list availible images
- docker diff  # list changes in filesystem
- docker build # build container from a Dockerfile
- docker inspect # low level  docker info on container
- docker logs #  STDOUT of main process
- docker attach #  interact with running container => basivcally run a
  buash on a running container and interact with it like with vm
- docker kill # kill main process of container
- docker start  <name| id> # starts existing docker container
- docker stop  <name| id> 
- docker ps  # list of running containers
- docker ps -a  # list of all containers including those that are not
  running
- docker login  # will login to docker-hub ...or other docker repo
  depending on settings default is docker hub
- docker rm a2cc01627771    # remove image



Dockerfile
- you can replace it with ansible, cheff,... as it is just simple bash
- each command executed creates a layer - if you done mistake on last
  cmd, you wont have to rebuild prev layers

- RUN # exec cmd in a shell
- VOLUME ['/data'] # enable access to host from working container , e.g.
  adding database.yml
- WORKDIR /path/to/workdir  #  set workdir in container
- ADD <src> <destination>  # copy files from one location to other
- CMD ['exec', 'stuff']  # default container execution (like rails
  server)
- ENV <key> <value>  # set env variables
- USER <uid>   # sets user that container is running as

- EXPOSE  123  # port container listen to
- 

image is exposing a port to docker-daemon but in order to really access
it you need to map ports to webserver 

- docker run -p 8080:80  tutum/hello-world  # create and run docker
  container + map web-server port 8080 to docker container port 80 

docker run -d --name web1 -p 8081:80 tutum/hello-world  # -d run as
daemon
                                                                                                              #
name it as web1
                                                                                                              #
map port web-server 8081 to port 80 of docker

docker run -d --name web2 -p 8082:80 tutum/hello-world 
docker run -d --name web3 -p 8083:80 tutum/hello-world 

docker ps  # will give you 3 images running
docker stop web2  
docker ps  # will give you 2 images running
docker start web2   


# sources and references:

[1]  3 hours to docker fundaments


1:14:49