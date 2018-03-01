This repository currently contains several [ROS packages](http://wiki.ros.org/Packages):

* [servicesim](https://bitbucket.org/osrf/servicesim/src/default/servicesim)
* [servicebot_control](https://bitbucket.org/osrf/servicesim/src/default/servicebot_control)
* [servicebot_description](https://bitbucket.org/osrf/servicesim/src/default/servicebot_description)
* [servicesim_competition](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition)
* [rqt_servicebot_pan_tilt](https://bitbucket.org/osrf/servicesim/src/default/servicesim_rqt_plugins/rqt_servicebot_pan_tilt)
* [rqt_servicesim_score](https://bitbucket.org/osrf/servicesim/src/default/servicesim_rqt_plugins/rqt_servicesim_score)
* [servicebot_2dnav](https://bitbucket.org/osrf/servicesim/src/default/competitor_example_solution/servicebot_2dnav)
* [servicesim_example_python_solution](https://bitbucket.org/osrf/servicesim/src/default/competitor_example_solution/competitor_example_solution)
* [servicesim_test](https://bitbucket.org/osrf/servicesim/src/default/servicesim_test)

***
# ServiceSim

[ServiceSim](https://bitbucket.org/osrf/servicesim/src/default/servicesim)
is the main entry point to run the competition. It provides a
[ROS launch file](http://wiki.ros.org/roslaunch) which is used to spin up the
Gazebo simulation and ROS controllers for ServiceBot.

Running the following command opens a window with the simulation running, sensor visualizations, a dashboard for control, and the robot will be ready to receive commands through the ROS interface.

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

***
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

The world generation is done using [embedded Ruby](https://en.wikipedia.org/wiki/ERuby) as explained on the [Scenario generation page](https://bitbucket.org/osrf/servicesim/wiki/Scenario%20generation).

File `service.world.erb` and other `.erb` files in the `servicesim_competition/worlds`
directory can be edited to add models, lights, configure human trajectories and so on.

## Gazebo plugins

There are several
[Gazebo plugins](http://gazebosim.org/tutorials?tut=plugins_hello_world)
within the competition package which are used to programmatically interact with
the simulation.

ServiceSim provides the following plugins:

* [CompetitionPlugin](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/src/CompetitionPlugin.hh): A world plugin which manages the flow of the competition and computes score
* [TrajectoryActorPlugin](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/src/TrajectoryActorPlugin.hh): A model plugin which is loaded for each human actor which makes them follow a given trajectory
  and stop when they approach an obstacle. The trajectory is configured on the SDF file, so it can be modified each time the simulation is run.
* [FollowActorPlugin](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/src/FollowActorPlugin.hh): A model plugin which is attached to the guest so it interacts with the robot and follows it, with a probability of deviating. Several parameters are also configurable via SDF.
* [VicinityPlugin](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/src/VicinityPlugin.hh): Provides the RFID sensor functionality

***
# ServiceBot description

The [ServiceBot description](https://bitbucket.org/osrf/servicesim/src/default/servicebot_description)
package contains the
[URDF](http://wiki.ros.org/urdf) model of ServiceBot. This package describes the robot's
geometry, kinematics and dynamics. It also loads the out-of-the-box [DifferentialDriveController](http://gazebosim.org/tutorials?tut=ros_gzplugins&cat=connect_ros#DifferentialDrive).

It is common for robot descriptions to be in their own `_description`
packages, see [pr2_description](http://wiki.ros.org/pr2_description) for example.

Keeping it separate from the rest of the ServiceSim software makes it convenient
to swap ServiceSim for another robot, all that is needed is that robot's own
description package.

***
# ServiceBot control

The [ServiceBot control](https://bitbucket.org/osrf/servicesim/src/default/servicebot_control)
package provides an interface to control the robot's joints.

***
# Custom RQT plugins (pan-tilt and score)

Package [rqt_servicebot_pan_tilt](https://bitbucket.org/osrf/servicesim/src/default/servicesim_rqt_plugins/rqt_servicebot_pan_tilt) provides the graphical widget to control the robot head joints.

Package [rqt_servicesim_score](https://bitbucket.org/osrf/servicesim/src/default/servicesim_rqt_plugins/rqt_servicesim_score) provides a widget to display the score on RQT.

***
# ServiceBot 2D Navigation

The [ServiceBot 2d Navigation](https://bitbucket.org/osrf/servicesim/src/default/competitor_example_solution/servicebot_2dnav) package leverages the ROS Navigation stack to make ServiceBot localize and do path planning in the world.

***
# ServiceSim example python solution

The [ServiceSim example python solution](https://bitbucket.org/osrf/servicesim/src/default/competitor_example_solution/competitor_example_solution) package serves as an example of how a competitor would solve the competition tasks.

***
# ServiceSim test

The [ServiceSim test](https://bitbucket.org/osrf/servicesim/src/default/servicesim_test) package uses the [ROS test suite](http://wiki.ros.org/rostest) to test the competition software and is tied to the [continuous integration](https://build.osrfoundation.org/view/proj_servicesim/) to ensure that new functionality doesn't break behaviour.