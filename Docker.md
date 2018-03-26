Running Servicesim in a docker container: 

## Requirements: ##

* An X-Server
* [Docker](https://docs.docker.com/install/#server)
* [Nvidia Docker](https://github.com/NVIDIA/nvidia-docker)

## Building: ##

First clone the servicesim repo, We are going to build a docker image for servicesim:

From `servicesim` folder do: 

`$ cd docker`

`$ ./build.sh`  

This builds the docker image for servicesim. 

## Running: ##

While still inside `servicesim/docker` folder, Run: 

`$ ./run.sh` 

Now do, `roslaunch servicesim servicesim.launch` to see the example world 

TIP: This docker image will have terminator, a linux terminal emulator with multiple terminals in one window, launching `terminator` will give the capability use mutiple terminals in a single docker container seamlessly. 

RUN :

` $ terminator`

` $ source /opt/ros/kinetic/setup.bash` , Remember to source this enviroment for each new terminal.