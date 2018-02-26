# Scenario generation

ServiceSim ships with an example scenario ready to be used, but it also provides a mechanism for generating custom scenarios as desired.

A scenario is defined by a combination `.world` and `.launch` files. The following explains how to generate new files based on a [config.yaml](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/worlds/config.yaml) file.

## Quick start

Follow these steps to locally generate and use a scenario.

1. Install Ruby:

        sudo apt-get update
        sudo apt-get install ruby2.3 ruby2.3-dev

1. Create a directory to hold the scripts and world files:

        mkdir ~/servicesim_worlds
        cd ~/servicesim_worlds

1. Copy the necessary script:
        
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/scenario.bash

1. Run the script:

        bash scenario.bash -d -p my_scenario

    > The *-d* flag tells the script to download files.
    > You just need to use this the first time you run the script or if you need to download updated templates.

1. This script should have generated two files, you can run the following to check:

        find `pwd` -name "my_scenario.*"

    And the output should be something like:

        /home/<user>/servicesim_worlds/my_scenario.world
        /home/<user>/servicesim_worlds/my_scenario.launch

1. To use the generated file, set the `custom` flag to true and pass the path prefix to the launch file, for example:

        roslaunch servicesim servicesim.launch custom:=true custom_prefix:=/home/<user>/servicesim_worlds/my_scenario



## Editing the configuration

The script downloaded a local copy of `config.yaml` for you, you can check its contents with:

    cat ~/servicesim_worlds/config.yaml

That file exposes several parameters to configure the competition scenario, such as the target rooms, the guest identity and configuration for guest drift.

Try changing the `targets: robot_start` property to `BackEntrance` and run the following to generate a new scenario:

    bash scenario.bash -p back_entrance

Now use that scenario and see how the robot starts near the back entrance:

    roslaunch servicesim servicesim.launch custom:=true custom_prefix:=/home/<user>/servicesim_worlds/back_entrance

If you delete or comment out options in the file, the template will pick them randomly.

## Advanced use

The `scenario.bash` script is calling the [service.world.erb](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/worlds/service.world.erb) template. It accepts the following options:

* **s**: Pass a seed to the random generator
* **f**: Set to true to generate only a floorplan of the world (no movable objects)
* **d**: Set to true to generate a world with debug visuals
* **urdf_launch**: Pass name of launch file which will spawn the robot URDF (`scenario.bash` does this for us)

You can directly call `erb`, or pass arguments to `scenario.bash` so they are forwarded to the template. 

For example, fix the seed at 100 and generate debug visuals:

    erb s=100 d=true urdf_launch=debug_100.launch service.world.erb > debug_100.world

You can get the same result with `scenario.bash` as follows:

    bash scenario.bash -t debug_100 -args "s=100 d=true"