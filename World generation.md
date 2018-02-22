# World generation

The world provided with the competition package ([service.world](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/worlds/service.world)) was generated from a the [service.world.erb](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/worlds/service.world.erb) template, which randomizes several parameters.

New worlds can be generated based on a [config.yaml](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/worlds/config.yaml) file.

1. Make sure you have a recent version of ruby installed (recommended > 2.2)

        ruby --version

1. In case you have an old version, you can upgrade as follows:

        sudo apt-get install software-properties-common python-software-properties
        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.2 ruby2.2-dev

1. Create a directory to hold the scripts and world files:

        mkdir ~/servicesim_worlds
        cd ~/servicesim_worlds

1. If you've done this before, first delete the old `erb` and `yaml` files:

        rm *.erb *.yaml

1. Copy the necessary `erb` templates and the `yaml` config:
        
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/actor_collisions.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/actor_idle.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/actor_trajectory.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/back_entrance.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/bathroom_furniture.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/chair.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/conference_table.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/config.yaml
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/cubicle_corner.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/cubicle_island.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/cubicles.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/debug_visuals.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/front_entrance.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/idle_near_entrance.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/idle_near_fridge.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/meeting_room_large_furniture.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/meeting_room_small_furniture.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/office_chair.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/office_large_furniture.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/office_small_furniture.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/private_cafe.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/refreshment_area_furniture.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/room.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/service.world.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/trajectory_back.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/trajectory_front.erb
        wget https://bitbucket.org/osrf/servicesim/raw/default/servicesim_competition/worlds/walls.erb

1. Generate a world as follows. Each time this command is run,
   a different world will be generated.

        erb service.world.erb > custom.world

    > Options:
    > 
    > * s: Pass a seed to the random generator, to always generate the same file
    > * f: Set to true to generate only a floorplan of the world
    > * d: Set to true to generate a world with debug visuals
    >
    > For example: erb s=100 d=true service.world.erb > debug_100.world

1. **TODO** To use one of the generated worlds, you must set the `USE_CUSTOM_WORLD`
   environment variable to true:

        export USE_CUSTOM_WORLD=1

1. **TODO** You also need to set another environment variable with the full path to the
   world file you wish to use, for example:

        export CUSTOM_WORLD_PATH=~/servicesim_worlds/custom.world

    *Obs: These commands will only set the environment variables for the current
     terminal. If you wish to set the variables for every new terminal, you can
     do:*

        echo "export USE_CUSTOM_WORLD=1" >> ~/.bashrc
        echo "export CUSTOM_WORLD_PATH=~/servicesim_worlds/custom.world" >> ~/.bashrc

1. Now you can use the usual launch file, and that will use the custom world:

        roslaunch servicesim servicesim.launch