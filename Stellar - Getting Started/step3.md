Upon launching a persistent mode container for the first time, the launch script will notice that the mounted volume is empty. This will trigger an interactive initialization process to populate the initial configuration for the container. This interactive initialization adds some complications to the setup process because in most cases you won't want to run the container interactively during normal operation, but rather in the background. We recommend the following steps to setup a persistent mode node:

1) Run an interactive session of the container at first, ensuring that all services start and run correctly.
2) Shut down the interactive container (using Ctrl-C).
3) Start a new container using the same host directory in the background.

To customize the configurations that both stellar-core and horizon use, you must use persistent mode. The default configurations will be copied into the data directory upon launching a persistent mode container for the first time. Use the diagram below to learn about the various configuration files that can be customized.

Image

It is recommended that you stop the container before editing any of these files, then restart the container after completing your customization.

NOTE: Be wary of editing these files. It is possible to break the services started within this container with an bad edit. It's recommended that you learn about managing the operations of each of the services before customizing them, as you are taking responsibility for maintaining those services going forward.

**Ports**

**Port  |      Service     |     Description**

5432    |     postgresql   |   database access port

8000    |     horizon      |      main http port

11625   |    stellar-core  |      main http port

11626   |    stellar-core  |      peer node port

**Security Considerations**

Exposing the network ports used by your running container comes with potential risks. While many attacks are preventable due to the nature of the stellar network, it is extremely important that you maintain protected access to the postgresql server that runs within a quickstart container. An attacker who gains write access to this DB will be able to corrupt your view of the stellar network, potentially inserting fake transactions, accounts, etc.

It is safe to open the horizon http port. Horizon is designed to listen on an internet-facing interface and has provides no privileged operations on the port.

The HTTP port for stellar-core should only be exposed to a trusted network, as it provides no security itself. An attacker that can make requests to the port will be able to perform administrative commands such as forcing a catchup or changing the logging level and more, many of which could be used to distrupt operations or deny service.

The peer port for stellar-core however can be exposed, and ideally would be routable from the internet. This would allow external peers to initiate connections to your node, improving connectivity of the overlay network. However, this is not required as your container will also establish outgoing connections to peers.
