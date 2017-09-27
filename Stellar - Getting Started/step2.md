When we launch our image, docker engine does not make full copy of already stored image. It just instantiates the container out of image i.e. it uses a technique called **copy-on-write mechanism**. It's a standard UNIX pattern that provides a single shared copy of data, until the data is modified.

To do this, changes between the image and the running container are tracked. Just before any write operation is performed in the running container, a copy of the file that would be modified is placed on the writable layer of the container(top most layer is writable), and that is where the write operation takes place. Hence the name, **“copy-on-write”**.

If this wasn’t happening, each time you launched an image, a full copy of the filesystem would have to be made. This would add time to the startup process and would end up using a lot of disk space.

Because of the copy-on-write mechanism, running containers can take less than 0.1 seconds to start up, and can occupy less than 1MB on disk. Compare this to Virtual Machines (VMs), which can take minutes and can occupy gigabytes of disk space, and you can see why Docker has seen such fast adoption.

But how is the copy-on-write mechanism implemented? To understand that, we need to take a look at the Union File System.
