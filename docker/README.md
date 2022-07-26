# Docker Containers

This directory (and below) are dedicated to docker containers for HPC. Based on initial evaluations, it seems that the best approach for managing a large number of containers would be to create docker containers and then import these into singularity as needed. As opposed to building singularity-specific containers. Either way they get to the same image type but many tools are Dockerized as opposed to singularity-ized. 

# tl;dr
To build an existing image and push to a local dockerhub:
```
cd r;make;make push
```

To create a new image:
- Create a new directory and copy Makefile/docker-compose.yml into it.
- Modify Makefile/docker-compose.yml as needed for new container.
- Create version directory and copy/create Dockerfile to create new container
- Then run the above commands to build/push container

# Overview
There are a number of steps in the development and deployment of a container: 

- developing the Dockerfile and docker-compose files
- building the image
- pushing image to local dockerhub
- retrieving image on cluster
- running the image

# Building the image
This is still in development. Based on my understanding at the moment, a docker compose file would allow us to hardcode the necessary tag for the image. For instance, in our example (see below for deploying to dockerhub) we need the image to be named:

```
dockerhub.moffitt.org/hpc/maxquant:2.0.3.1
```

Without any other ideas, it seems like if we hard-code this in the compose file then a docker compose build would build the necessary image in the local docker registry. Which can then be pushed to the dockerhub using commands in the next section.

The command is:
```
docker compose build
```

You can check the success of the process by looking for the built image in your local registry:
```
docker image ls
```



# Dockerhub
This step assumes that the container has been built on the local machine (in the local docker registry). You can check this:
```
docker image ls
```

For our internal operations, we use a local dockerhub instance (http://dockerhub.moffitt.org). It is a harbor server. The organization of this server (at the moment) is still in flux. However for the purposes of the example we have an open repository called `hpc`. This is the target to upload our local docker image into this dockerhub hpc project.

The docker image must be named in a certain way in order to be pushed to the appropriate place. The naming should be:
```
dockerhub.moffitt.org/hpc/maxquant:2.0.3.1
```

The command to upload to the local dockerhub is then
```
docker push dockerhub.moffitt.org/hpc/maxquant:2.0.3.1
```

Docker should then upload this to the hpc directory. Note that at some point in the future, the hpc directory may be write-restricted so that an additional layer of authentication is required.

# Makefiles
I have started implementing Makefiles for the container application. That is, there is a makefile in the R directory which will build each of the R/r-4.1, etc images. So you can type 
```
make r-4.1
```
in the R directory.


It also provides a mechanism for the "latest" version being specified in the Makefile. In the Makefile, it's just tagging that particular version as "latest" as well. This way when you push the images to dockerhub there will be "latest" to refer to.

Finally, there is a 
```
make push
```
which pushes the images (including the latest tag) to the dockerhub server.

# Running the Image: RED
Once the image has been pushed to the local dockerhub, you can access it via the RED cluster. Since the hub is (currently) open access, you can pull the image by the following:
```
singularity pull docker://dockerhub.moffitt.org/hpc/maxquant:2.0.3.1
```

