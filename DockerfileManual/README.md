# Dockerfile Manual

# FROM: 
The FROM instruction specifies the base image to use for creating the new image. It is the first instruction in a Dockerfile and is mandatory.  This line tells Docker to use the Ubuntu 20.04 image as the base for your new image.  
> FROM ubuntu:20.04  

# LABEL
> LABEL adds metadata to an image, such as a description, version, or maintainer details.  
> LABEL maintainer="you@example.com"  
> LABEL version="1.0"  
> LABEL description="A simple Ubuntu-based Docker image."  

# ARG
Inside Dockerfile, create argument for any variable like port  
> ARG PORT=3000  
> ENV PORT=${PORT}  
> EXPOSE ${PORT}  
For building the image, use below command, where PORT is an environment variable  
$ sudo docker build --build-arg PORT=8080 -t myapp:latest .  
Now run the container from the image  
$ sudo docker run -p 8080:8080 myapp:latest  

# RUN
The RUN instruction executes commands in a new layer on top of the current image and commits the results. It is commonly used to install software packages. This line updates the package list and installs curl and vim.  
> RUN apt-get update && apt-get install -y curl vim  
> RUN ["<executable>", "<param1>", "<param2>"]  

# COPY / ADD
COPY and ADD are used to copy files from the host system to the Docker image. COPY is generally preferred because it has a more straightforward behavior. ADD has some additional features like extracting TAR files and handling URLs. This command copies the current directory from the host machine to the /app directory in the Docker image.  
> COPY . /app  

# WORKDIR
WORKDIR sets the working directory for any RUN, CMD, ENTRYPOINT, COPY, and ADD instructions that follow it.  
> WORKDIR /app  

# EXPOSE
The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime. This exposes port 8080 to the outside world.  
> EXPOSE 8080  

# ENV
ENV sets environment variables. This sets the APP_ENV environment variable to production.  
> ENV APP_ENV=production  

# CMD
The CMD instruction specifies the default command to run when the container starts. If a different command is provided when starting the container, the CMD will be overridden. This runs python app.py when the container starts.  
> CMD ["python", "app.py"]  
> CMD ["<executable>","<param1>","<param2>"]

# ENTRYPOINT
The ENTRYPOINT instruction is similar to CMD but is not overridden when additional command-line arguments are provided.  
> ENTRYPOINT ["python", "app.py"]  
> ENTRYPOINT ["<executable>", "<param1>", "<param2>"]  

# VOLUME
Volumes can be managed by Docker, and they are typically stored outside of the container's writable layer. This isolation helps improve performance and data management, and also ensures that the data is not accidentally lost when a container is removed.  
VOLUME creates a mount point with the specified path and marks it as holding externally mounted volumes from the host or other containers. This declares /data as a mount point.  
VOLUME /data specifies that the directory /data inside the container will be mounted as a volume. This is where log files are stored for example.  
> VOLUME /data  
Now, you use above VOLUME at the time of creating container to map it with host machine directory. You can run a container and map the volume to a specific directory on the host machine:  
> $ sudo docker run -d -v /home/admin/data:/data -p 3306:3306 myimage:tag8.0  

# USER
The USER instruction sets the user name or UID to use when running the image. This switches to the appuser user.  
> USER appuser  

# HEALTHCHECK
The HEALTHCHECK instruction tells Docker how to test the container to check that it is still working.  
> HEALTHCHECK --interval=30s --timeout=5s CMD curl -f http://localhost/ || exit 1  

# STOPSIGNAL 
from stopping the docker mentioned signal to be used. The image's default stopsignal can be overridden per container, using the --stop-signal flag on docker run and docker create.  
> STOPSIGNAL SIGKILL  
  