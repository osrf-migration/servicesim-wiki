This repository currently contains 3 ROS packages:

* [servicesim](https://bitbucket.org/osrf/servicesim/src/default/servicesim)
* [servicebot_description](https://bitbucket.org/osrf/servicesim/src/default/servicebot_description)
* [servicesim_competition](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition)

# ServiceSim

[ServiceSim](https://bitbucket.org/osrf/servicesim/src/default/servicesim)
is the main entry point to run the competition. It provides a
[ROS launch file](http://wiki.ros.org/roslaunch) which is used to spin up the
Gazebo simulation and ROS controllers for ServiceBot.

Running the following command will open a window with the simulation running
and the robot will be ready to receive commands through the ROS interface.

~~~
roslaunch servicesim servicesim.launch
~~~

Any other ROS nodes which should be launched together with the simulation can
be added to [servicesim.launch](https://bitbucket.org/osrf/servicesim/src/default/servicesim/launch/servicesim.launch),
but they can also be launched separately, for example calling
[rosrun](http://wiki.ros.org/rosbash#rosrun).

This package is meant to work as a central entry-point and doesn't provide much
functionality itself. This way, it can be configured to spin up, for example,
the same competition but with a different robot.

# ServiceSim Competition

The [ServiceSim Competition](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition)
package provides everything that is needed to run the competition, such as
worlds, models and Gazebo plugins. This package is robot-agnostic, so
it can be used with other robots besides ServiceBot.

## Launch

The `servicesim.launch` file from the `servicesim` package is configured to
launch the
[competition.launch](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/launch/competition.launch)
file from the `servicesim_competition` package.

This launch file is responsible for spinning up the Gazebo simulation specific
to the competition.

## Worlds

When roslaunch spins up Gazebo, it passes the
[service.world](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/worlds/service.world)
file. This is the Gazebo world file in [SDF (Simulation Description Format)](http://sdformat.org/spec)
where many details of the world are described, such as:

* Static and dynamic models (office and other objects) and their properties,
  such as position and shape.
* Lights and their properties, such as color and direction.
* Environment properties, like gravity and physics engine parameters.
* Human actors and their properties, such as animation and skin files.
* Gazebo plugins to be loaded, explained in more detail below.

The `service.world` file is quite long and complex, therefore, instead of
creating it manually, it is convenient to automatically generate it from a scripted
template. That is the
[service.world.erb](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/worlds/service.world)
file.

The world generation is done using [embedded Ruby](https://en.wikipedia.org/wiki/ERuby).
You can install Ruby 2.2 as follows:

    sudo apt-get install software-properties-common python-software-properties
    sudo apt-add-repository ppa:brightbox/ruby-ng
    sudo apt-get update
    sudo apt-get install ruby2.2 ruby2.2-dev

And then run the following command to generate a new `service.world` from
`service.world.erb`:

~~~
erb servicesim_competition/worlds/service.world.erb > servicesim_competition/worlds/service.world
~~~

File `service.world.erb` and other `.erb` files in the `servicesim_competition/worlds`
directory can be edited to add models, lights, configure human trajectories and so on.

## Gazebo plugins

There will be several
[Gazebo plugins](http://gazebosim.org/tutorials?tut=plugins_hello_world)
within the competition package which are used to programmatically interact with
the simulation.

These are some of the plugins which will become part of ServiceSim:

* A world plugin which manages the flow of the competition and computes score
* One plugin for each human actor which makes them follow a given trajectory
  and stop when they approach an obstacle. The trajectory is configured on the SDF
  file, so it can be modified each time the simulation is run.
* One plugin for the guest so it interacts with the robot and follows it, with
  a probability of deviating. All parameters about the guest are also configurable
  via SDF.


# ServiceBot description

The [ServiceBot description](https://bitbucket.org/osrf/servicesim/src/default/servicebot_description)
package contains the
[URDF](http://wiki.ros.org/urdf) model of ServiceBot. This package describes the robot's
geometry, kinematics and dynamics.

It is common for robot descriptions to be in their own `_description`
packages, see [pr2_description](http://wiki.ros.org/pr2_description) for example.

Keeping it separate from the rest of the ServiceSim software makes it convenient
to swap ServiceSim for another robot, all that is needed is that robot's own
description package.
