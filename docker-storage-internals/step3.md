The **Union File System(UFS)** specializes in **not storing duplicate data.**

If two images have identical data, that data does not have to be recorded twice on disk. Instead, you can store the data once and then use it in many locations. This is possible with something called a layer.

Each layer is a file system, and as the name suggests, they can be layered on top of each other. Crucially, single layers containing shared files can be used in many images. This allows images to be constructed and deconstructed as needed, via the composition of different file system layers.

The layers that come with an image you pull from the Docker Hub are read-only. But when you run a container, you add a new layer on top of that. And the new layer is writable.

When you write to that layer, the entire stack is searched for the file you are writing to. And if a file is found, it is first copied to the writable layer. The write operation is then performed on that layer, not the underlying layer.

This works because when reading from a UFS volume, a search is done for the file that is being read. The first file that is found, reading from top to bottom, is used. So files on the writable layer of your container are always used.

If we were to run thousands of containers based on the same base layers we reap huge benefits in both startup time and disk space.

One example setup that would benefit is a web app that horizontally scales many identical web servers. Another would be a hosting company that provides the same basic image to all customers, and then only writes the data that customers add or change.

Simply pull two different docker images of alpine:3.3 and alpine:latest and verify that the intermediate similar layers store once on the local memory.
`docker pull alpine:3.3`{{execute}}

`docker pull alpine:latest`{{execute}}
