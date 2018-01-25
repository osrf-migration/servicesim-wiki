The ServiceSim simulation consists of a few files:

## Launch files

A [ROS launch file](http://wiki.ros.org/roslaunch) is used to spin up the
Gazebo simulation and ROS controllers for ServiceBot.

Running the following command will open a window with the simulation running
and the robot will be ready to receive commands through the ROS interface.

~~~
roslaunch servicesim servicesim.launch
~~~

Any other ROD nodes which should be launched together with the simulation can
be added to `servicesim.launch`, but they can also be launched separately, for
example calling [rosrun](http://wiki.ros.org/rosbash#rosrun).

## Worlds

When roslaunch spins up Gazebo, it passes the `servicesim.world` file. This is the
Gazebo world file in [SDF (Simulation Description Format)](http://sdformat.org/spec)
where many details of the world are described, such as:

* Static and dynamic models (office and other objects) and their properties,
such as position and shape.
* Lights and their properties, such as color and direction.
* Environment properties, like gravity and physics engine parameters.
* Human actors and their properties, such as animation and skin files.
* Gazebo plugins to be loaded, explained in more detail below.

* ERB

## Plugins

    * A world plugin which manages the flow of the competition and computes score
      (`CompetitionPlugin`)
    * One plugin for each human actor which makes them follow a given trajectory
      and stop when they approach an obstacle (`TrajectoryActorPlugin`)
    * One plugin for the






