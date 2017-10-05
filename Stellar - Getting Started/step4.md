There will come a time when you want to inspect the running container, either to debug one of the services, to review logs, or perhaps some other administrative tasks. We do this by starting a new interactive shell inside the running container:

`docker exec -it stellar /bin/bash`{{execute}}

The command above assumes that you launched your container with the name stellar; Replace that name with whatever you chose if different. When run, it will open an interactive shell running as root within the container.

**Restarting services**

Services within the quickstart container are managed using supervisord and we recommend you use supervisor's shell to interact with running services. To launch the supervisor shell, open an interactive shell to the container and then run **supervisorctl**. You should then see a command prompt that looks like:

`supervisorctl`{{execute}}

**Note** : If you receive error as **unix:///var/run/supervisor.sock no such file** then apparently run "service supervisord start" doesn't necessarily load your config file, or even a config file at all. In order to make it work, I had to do a **supervisord -c /stellar/supervisor/etc/config.conf** (i.e. run the binary directly) this fixed the error.

horizon                          RUNNING    pid 143, uptime 0:01:12
postgresql                       RUNNING    pid 126, uptime 0:01:13
stellar-core                     RUNNING    pid 125, uptime 0:01:13
supervisor>

From this prompt you can execute any of the supervisor commands:

# restart horizon
`restart horizon`{{execute}}


# stop stellar-core
`stop stellar-core`{{execute}}

You can learn more about what commands are available by using the help command.

**Viewing logs**

Logs can be found within the container at the path `/var/log/supervisor/`. A file is kept for both the stdout and stderr of the processes managed by supervisord. Additionally, you can use the `tail` command provided by supervisorctl.

**Accessing databases**

The point of this project is to make running stellar's software within your own infrastructure easier, so that your software can more easily integrate with the stellar network. In many cases, you can integrate with horizon's REST API, but often times you'll want direct access to the database either horizon or stellar-core provide. This allows you to craft your own custom sql queries against the stellar network data.

This image manages two postgres databases: `core` for stellar-core's data and `horizon` for horizon's data. The username to use when connecting with your postgresql client or library is `stellar`. The password to use is dependent upon the mode your container is running in: Persistent mode uses a password supplied by you and ephemeral mode generates a password and prints it to the console upon container startup.