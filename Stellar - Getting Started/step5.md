Below is a list of various ways you might want to launch the quickstart container annotated to illustrate what options are enabled. It's also recommended that you should learn and get familiar with the docker command.

Launch an ephemeral pubnet node in the background(Note: In your current scenario stellar is already running, give it another name):

`docker run -d -p "8000:8000" --name stellar stellar/quickstart --pubnet`{{execute}}

Launch an ephemeral testnet node in the foreground, exposing all ports:

`docker run --rm -it \
    -p "8000:8000" \
    -p "11626:11626" \
    -p "11625:11625" \
    --name stellar \
    stellar/quickstart --testnet`{{execute}}

Setup a new persistent node using the host directory */str*:

`docker run -it --rm \
    -v "/str:/opt/stellar" \
    --name stellar \
    stellar/quickstart --pubnet`{{execute}}

Start a background persistent container for an already initialized host directory:

`docker run -d \
    -v "/str:/opt/stellar" \
    -p "8000:8000" \
    --name stellar \
    stellar/quickstart --pubnet`{{execute}}
