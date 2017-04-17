A volume is a directory mounted inside a container that exists outside of the union file system. They are created via a Dockerfile, or the Docker CLI tool. The volume can map to an existing directory on the host machine, or remote NFS device.

The directory a volume maps to exists independently from any containers that mount it. This means you can create containers, write to volumes, and then destroy the containers again, without fear of losing any app data.

Volumes are great when you need to share data (or state) between containers, by mounting the same volume in multiple containers. Though take note: it’s important to implement locks or some other concurrent write access protection.

**“Volumes are great when you need to share data (or state) between containers…”**

They’re also great when you want to share data between containers and the host machines, for example accessing source code.

Another common use is of volumes is when you’re dealing with large files, such as logs or databases. That’s because writing to a volume is faster than writing to the union file system, which uses the (IO expensive) copy-on-write mechanism.

To demonstrate the power of volumes and how to use them, let’s look at two scenarios.

*1) RUNNING A CONTAINER WITH A VOLUME FLAG*

 Launch a container with -v, the volume flag:

 `docker run -d -v /code -p 8080:80 --name mynginx nginx`{{execute}}

This creates a procedural named directory (which we will look at shortly) on the host machine and then maps it to the /code directory in the container. You can see the volume has been created and mounted with this command:

`docker inspect mynginx`{{execute}}

You should see a long JSON-like output onto the terminal.

This output confirms the creation of the volume at the docker engine level as well as the mapping to the container’s **/code** directory. Also take note of **/var/lib/docker/volumes/12f6[...]/_data**, being the the volume path. We will use this path to access our data on the host machine.

Okay, next, grab a shell inside the container:

`docker exec -it mynginx /bin/bash`{{execute}}

Check the /code directory exists:

`ls`{{execute}}

Change to the **/code** directory:

`cd code`{{execute}}

Write something to a test file, *myfile*:

`echo Hello > myfile`{{execute}}

And exit the container:

`exit`{{execute}}

Cool. So we just wrote some data to a file in the volume mount inside our container. Let’s look in that directory on the host machine we saw in the docker inspect output above to see if we can find the data we wrote.

Login as the superuser, so you can access the Docker lib files:

`ssh root@host01`{{execute}}

Now, change to the directory listed in the previous docker inspect output:

**Note: The ID in the below command may be different in your case. Get the respective ID for your volume and then execute the command.**

`cd /var/lib/docker/volumes/12f6b6d488484c65bedcda8300166d76e6879a496ce2d0742ab23981621c8b1a/_data`{{execute}}

Check the contents of the directory:

 `ls`{{execute}}

Bingo! That’s the file we created inside the container.

You can even run **`cat myfile`{{execute}}** if you want to check the contents are the same. Or additionally, you could modify the contents here and then grab a shell inside the container and check that it has been updated there.

You can come out of sudo using simple command,

`exit`{{execute}}

*2) CREATE ENGINE LEVEL VOLUMES AND STORAGE FOR TRANSIENT CONTAINERS*

Since Docker 1.9, it is possible to create volumes using the Docker API.

You can create a volume via the Docker API like this:

`docker volume create --name myvolume`{{execute}}

We can check it worked like so:

`docker volume inspect myvolume`{{execute}}

Notice the Mountpoint into the inspect command.

Now, let’s run a little test:

`docker run -d -v myvolume:/data busybox sh -c "echo Hello > /data/myfile.txt"`{{execute}}

What’s happening here?

First, we launch a **busybox** container and mount the **myvolume** volume to the **/data** directory. Then we execute a command inside the container that writes “Hello” to the **/data/myfile.txt** file. After that command has run, the container is stopped.

You can modify the above command to run **cat /data/myfile.txt** if you want to read the data from inside the container at any point.

So, let’s see if we can find that file on our host machine.

Log in as the superuser:

`ssh root@host01`{{execute}}

Then change directory to the path listed as the **Mountpoint** in the output from the **docker volume inspect myvolume** command above.

`cd /var/lib/docker/volumes/myvolume/_data`{{execute}}

And again, check the contents:

`ls`{{execute}}

You can then check that file **myfile.txt** present and you could read this file, write to it, and so on. And everything you do will be reflected inside the container. And vice versa. This way docker storage internals work and if you keen you can hack your storage. Also you can mount the volumes as when you want as per your requirements. 
