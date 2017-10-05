Stellar provides a simple way to incorporate **stellar-core** and **horizon** into your private infrastructure, provided that you use docker.

This image provide a default, non-validating, ephemeral configuration that should work for most developers. By configuring a container using this image with a host-based volume an operator gains access to full configuration customization and persistence of data.

The image uses the following software:

    1) Postgresql 9.5 is used for storing both stellar-core and horizon data
    2) stellar-core
    3) horizon
    4) Supervisord is used from managing the processes of the services above.

First, decide whether you want your container to be part of the public, production Stellar network (referred to as the pubnet) or the test network (called testnet) that we recommend you use while developing software because you need not worry about losing money on the testnet. You'll provide either --pubnet or --testnet as a command line flag when starting the container to determine which network (and base configuration file) to use.

Next, you must decide whether you will use a docker volume or not. When not using a volume, we say that the container is in ephemeral mode, that is, nothing will be persisted between runs of the container. Persistent mode is the alternative, which should be used in the case that you need to either customize your configuration (such as to add a validation seed) or would like avoid a slow catchup to the Stellar network in the case of a crash or server restart. We recommend persistent mode for anything besides a development or test environment.

Finally, you must decide what ports to expose. The software in these images listen on 4 ports, each of which you may or may not want to expose to the network your host system is connected to. A container that exposes no ports isn't very useful, so we recommend at a minimum you expose the horizon http port.

**Ephemeral mode**

`docker run -d --rm -it -p "8000:8000" --name stellar stellar/quickstart --testnet`{{execute}}

**Persistent mode**

`docker run -d --rm -it -p "8000:8000" -v "/home/mohan/stellar:/opt/stellar" --name stellar stellar/quickstart --testnet`{{execute}}

The -v option in the example above tells docker to mount the host directory /home/mohan/stellar into the container at the /opt/stellar path. You may customize the host directory to any location you like, simply make sure to use the same value every time you launch the container. Also note: an absolute directory path is required. The second portion of the volume mount (/opt/stellar) should never be changed. This special directory is checked by the container to see if it is mounted from the host system which is used to see if we should launch in ephemeral or persistent mode.
