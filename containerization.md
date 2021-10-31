# containerization
```bash
docker pull          # pull an image or a repository from a registry;

docker run --detach --publish 8080:8080 --volume jenkins_home:/var/jenkins_home --name jenkins jenkins/jenkins:lts

docker run           # run a command in a new container;
docker run --detach  # run container in background and print container id;
docker run --publish # publish a container's port(s) to the host;
docker run --volume  # bind mount a volume;
docker exec          # run a command in a running container;

docker images -f dangling=true -q # check unused docker images
# therefore we can pipe above command into a subshell to cleanup dangling images
docker rmi $(docker images -f dangling=true -q)

# almost same thing with the containers
docker ps -aq # shows all container IDs
docker rm $(docker -aq) # removes all containers (it has to be stopped first)
```
