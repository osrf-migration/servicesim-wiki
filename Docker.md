Running ServiceSim in a docker container

## Requirements

* An X-Server
* [Docker](https://docs.docker.com/install/#server)
* [Nvidia Docker version 1.0](https://github.com/NVIDIA/nvidia-docker/wiki/Installation-(version-1.0))

## Building

We are going to build a docker image for ServiceSim.

First clone the `servicesim` repo:

    hg clone https://bitbbucket.org/osrf/servicesim

Move to the docker folder:

    cd servicesim/docker

Run the build script:

    ./build.sh

## Running

While still inside `servicesim/docker` folder, Run: 

    ./run.sh 

Now you're inside a new docker container. From within you can run
the following to see the example world:

    roslaunch servicesim servicesim.launch