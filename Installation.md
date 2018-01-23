# Install and run

## Installation

Installation instructions for Ubuntu Xenial (16.04)

1. Install Gazebo 8

    TODO

1. Install ROS Kinetic

    TODO

1. Install ServiceSim

    TODO

## Running example

Run the example world as follows

     cd servicesim
     GAZEBO_MODEL_PATH=`pwd`/models:$GAZEBO_MODEL_PATH gazebo --verbose worlds/service.world

## Generating new worlds

     cd servicesim/worlds
     erb service.world.erb > service.world