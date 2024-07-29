# Docker Manual

# docker install
> $ sudo apt-get install docker.io  

# creating docker image
> $ sudo docker build -t [REPOSITORY]:[TAG] . [currently directory must contain Dockerfile]  
[options]  
-t, --tag [Name and optionally a tag in the name:tag format.]  
> $ sudo docker build -t myimage:latest . [use the tag]  
-f, --file [provided the path of Dockerfile]  
> $ sudo docker build -f Dockerfile.dev .   
--build-arg [Set build-time variables.] [Read more in Dockerfile concept]  
> $ sudo docker build --build-arg HTTP_PROXY=http://proxy.example.com .  
--pull [Always attempt to pull a newer version of the base image.]  
> $ sudo docker docker build --pull .  
--label [Set metadata for an image.]  
> $ sudo docker build --label com.example.version="1.0" .  
--network [Set the networking mode for the RUN instructions during build.]  
> $ sudo docker build --network host .  
--output [Output destination (e.g., local,dest=path).]  
> $ sudo docker build --output type=local,dest=./output .  
--target [Set the target build stage to build (useful in multi-stage builds).]  
> $ sudo docker build --target builder .  
--platform [Set the platform if the server is multi-platform capable.]  
> $ sudo docker build --platform linux/amd64 .  

# docker list images  
[-f provided for filter: --filter]: ancestor, before, after, dangling etc  
> $ sudo docker images [list all currently built docker images]  
or  
> $ sudo docker images ls  
> $ sudo docker images REPOSITORY:TAG [list docker images with repo name and tag provided]  
> $ sudo docker images --filter "dangling=true" [list docker images without repo name and tag]  
> $ sudo docker images --filter "before=image1" [list docker images created before image1]  
> $ sudo docker images --filter "after=image1" [list docker images created after image1]  

# docker create containers
--name [name the container]  
> $ sudo docker run --name mycontainer myimage:tag  
-p, --publish [Publish a container's port(s) to the host.]  
> $ sudo  docker run -p 8080:80 myimage:tag   
-e, --env [Set environment variables.]  
> $ sudo docker run -e MY_ENV_VAR=value myimage:tag  
-v, --volume [Bind mount a volume.]  
> $ sudo docker run -v /host/path:/container/path myimage:tag  
--rm [Automatically remove the container when it exits.]  
> $ sudo docker run --rm myimage:tag  
-h, --hostname [Assign a hostname to the container.]  
> $ sudo docker run -h myhostname myimage:tag  
--network [Connect the container to a specific network.]  
> $ sudo docker run --network mynetwork myimage:tag  
--restart [Restart policy to apply when a container exits (e.g., no, on-failure, always, unless-stopped).]  
> $ sudo docker run --restart unless-stopped myimage:tag  

# docker list containers
[-a provided for all containers: --all]  
[-f provided for filter: --filter]: status, exited, ancestor, before, after, label, health, network etc  
> $ sudo docker ps [list all running docker containers]  
> $ sudo docker ps -a [list all docker containers] [-a stands for --all]  
> $ sudo docker ps --filter status=running [or restarting, paused, exited, created etc]  
> $ sudo docker ps -a --filter 'exited=137' [list docker containers exited with 137 status]  
> $ sudo docker ps --filter ancestor=ubuntu [list containers who have ubuntu as ancestor]  
> $ sudo docker ps -f before=9c3527ed70ce [list the containers created before provided container id]  
> $ sudo docker ps -f after=9c3527ed70ce [list the containers created after provided container id]  
> $ sudo docker ps --filter "label=color=blue" [list the containers with color label with blue value]  
> $ sudo docker ps --filter health=healthy [starting, healthy, unhealthy or none]  
> $ sudo docker ps --filter network=net1 [list the containers running on network net1]  

# others
Create Network for docker container to run as a family  
> $ sudo docker network create my_network  
Running a Command in a Container  
> $ sudo docker run -it ubuntu /bin/bash    
Stopping a container  
> $ sudo docker stop mycontainer  
Removing a container  
> $ sudo docker rm mycontainer  
Start one or more stopped containers.  
> $ sudo docker start mycontainer  
Restart one or more containers.  
> $ sudo docker restart mycontainer  
Pause all processes within one or more containers.  
> $ sudo docker pause mycontainer  
Unpause all processes within one or more containers.  
> $ sudo docker unpause mycontainer  
Kill one or more running containers (sends SIGKILL).  
> $ sudo docker kill mycontainer  
Fetch the logs of a container.  
> $ sudo docker logs mycontainer  
Display detailed information on one or more containers.  
> $ sudo docker inspect mycontainer -f, --format json  
Display a live stream of resource usage statistics for containers.  
> $ sudo docker stats mycontainer  
Display the running processes of a container.  
> $ sudo docker top mycontainer  
Force remove a running container (sends SIGKILL).  
> $ sudo docker rm -f mycontainer  
Remove unused Docker objects.  
docker container prune (Removes all stopped containers)  
List port mappings or a specific mapping for a container.  
> $ sudo docker port mycontainer  
Manage Docker networks.  
> $ sudo docker network ls (Lists all networks)  
Export a container's filesystem as a tar archive.  
> $ sudo docker export mycontainer > mycontainer.tar  
Import a tarball to create a filesystem image.  
> $ sudo docker import mycontainer.tar myimage  
Rename a container  
> $ sudo docker rename my_container my_new_container  
  
