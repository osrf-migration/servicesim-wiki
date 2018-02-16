Create a 2D floor map of the world:

* Download the source code: `hg clone https://bitbucket.org/osrf/collision_map_creator_plugin`.

*  Install the dependency package, protobuf-compiler: 
```
#!bash

sudo apt-get install protobuf-compiler

```
### Build and Deploy ###
*  To build this project, create a build directory, run CMake and then make:

```
#!bash

cd ~/collision_map_creator_plugin
mkdir build
cd build
cmake ../
make

```

* This plugin needs to be added to the gazebo plugin path. You can either change your environment variable to refer to this build directory 

```
#!bash

export GAZEBO_PLUGIN_PATH=$GAZEBO_PLUGIN_PATH:collision_map_creator_plugin/build

```
or you can copy the plugin to your plugin directory.


```
#!bash

sudo cp libcollision_map_creator.so /usr/lib/gazebo-<YOUR-GAZEBO_VERSION>/plugins/

```
### Running ###
*  Modify the world file `services.world` to add the plugin to the world tag:
  `<plugin filename="libcollision_map_creator.so" name="collision_map_creator"/>` 

*   In a separate terminal, run the executable and tell it to build a 30m x 30m map with a 5cm resolution.

```
#!bash
~/collision_map_creator_plugin/build/request_publisher "(-30,30)(30,30)(30,-30)(-30,-30)" 10 0.05 ~/map.png


```
*  Follow the tutorials in [map_server](Link http://wiki.ros.org/map_server) to load and visualize the map in rviz.