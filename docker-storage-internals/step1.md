Before going to the tutorial, Can you think on the question, **How docker stores the images internally ?**

There are lot of place inside docker both at **engine level** and **container level** that use or work with storage. Let's deep dive into the storage.

Let’s imagine we want to pull a Docker image from a registry, like so:

`docker pull nginx`{{execute}}

When you hit enter, docker search for the respective image into local repository, if it's not found, docker will pull the nginx image from the Docker Hub. At Docker Hub, you can see all the images with versions and its respective Dockerfile. Once the pulling completes, it will added into your local repository and managed by docker engine.

We can verify this is the case by listing the local images:

`docker images`{{execute}}

Now if we launch nginx image, it will spin up quickly as its store locally.

We can launch it like so,

`docker run -d --name web1 -p 8081:80 nginx`{{execute}}

This command maps port 80 of the container to port 8081 of the host machine. After it has run, you can connect at port 8081 on host(**docker** is the host in our scenario) to verify that **nginx** responds. Just run the next command,

`curl http://docker:8081/`{{execute}}

This step we can easily visualize, but whats happening behind the scene, as far as this containers file system ? To understand it we need to look at the copy-on-write mechanism.
