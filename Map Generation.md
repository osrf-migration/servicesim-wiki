## Create a 2D floor map of the world: ##

Instructions copied from [here](http://gazebosim.org/tutorials?tut=custom_messages#BuildandDeploy) and modified

### Get the code and dependencies ###

* Download the source code into a `<path>` of your choice:

        cd <path>
        hg clone https://bitbucket.org/osrf/collision_map_creator_plugin


*  Install the dependency package, protobuf-compiler: 

        sudo apt-get install protobuf-compiler

### Build and Deploy ###

*  To build this project, create a build directory, run CMake and then make:

        cd <path>/collision_map_creator_plugin
        mkdir build
        cd build
        cmake ..
        make -j$( getconf _NPROCESSORS_ONLN )

* This plugin needs to be added to the gazebo plugin path. You can either change your environment variable to refer to this build directory 

        export GAZEBO_PLUGIN_PATH=$GAZEBO_PLUGIN_PATH:`pwd`

    or you can copy the plugin to your plugin directory.

        sudo cp libcollision_map_creator.so /usr/lib/gazebo-<YOUR-GAZEBO_VERSION>/plugins/

### Running ###

1. Within the same shell as before, navigate to `servicesim/servicesim_competition`:

        cd <path_to>/servicesim/servicesim_competition

1.  Modify the floorplan world [servicesim_competition/worlds/floorplan.world](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/worlds/floorplan.world) to add the plugin to the `<world>` tag:

        <plugin filename="libcollision_map_creator.so" name="collision_map_creator"/>

1. Source Gazebo 8's setup file (important because we'll be setting `GAZEBO_RESOURCE_PATH`). From a debian install, it should be:

        . /usr/share/gazebo-8/setup.sh

1. In the same terminal open the modified floorplan world in gazebo, while setting a few environment variables to be sure we find all the necessary resources (be sure to run this from `servicesim/servicesim_competition`):


        GAZEBO_MODEL_PATH=`pwd`/models:$GAZEBO_MODEL_PATH GAZEBO_RESOURCE_PATH=`pwd`/media:$GAZEBO_RESOURCE_PATH gazebo --verbose worlds/floorplan.world

 
1. In a separate terminal, run the executable and tell it to build a 60m x 60m map with a 5cm resolution.

        cd <path>
        ./collision_map_creator_plugin/build/request_publisher "(-30,30)(30,30)(30,-30)(-30,-30)" 10 0.05 ~/map.png

1. See the map image in your home folder.

1. Follow the tutorials in [map_server](http://wiki.ros.org/map_server) to load and visualize the map in rviz.