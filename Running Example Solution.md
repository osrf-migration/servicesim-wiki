We provide an example solution to the competition to illustrate how to use the ROS interfaces and how you could structure your own solution.

This tutorial will show you how to run the example and explain the code within the example.

### Prerequisites

Before doing this tutorial you need to have installed `servicesim` from the debian files via `apt`, as described on the [Installation Page](https://bitbucket.org/osrf/servicesim/wiki/Installation).

### Running the Competition

Before running the solution, we need to start the competition:

```
# in a new terminal
$ source /opt/ros/kinetic/setup.bash
$ roslaunch servicesim servicesim.launch rviz:=false teleop:=false
```

This will launch `gazebo` and the `rqt` dashboard, but it prevents the keyboard teleoperation from starting (since we'll be controlling autonomously), as well as preventing `rviz` from starting since our example solution has a different `rviz` config which is nicer when using the navigation stack, which our example uses.

### Running the Example Solution

Once the competition software has started, we can run the example competition solution:

```
# in a new terminal
$ source /opt/ros/kinetic/setup.bash
$ roslaunch servicesim_example_python_solution example_solution.launch
```

This will run a few things:

- the [ROS navigation stack](http://wiki.ros.org/navigation), which we use to autonomously navigate the robot
- `rviz` with a custom display configuration
- the example solution, `example_solution.py`, which we'll go over in detail later

### Observe the Solution

TODO: things they should see the example solution doing

### Next Tutorial

The next tutorial will describe how you can get a local working copy of our example solution which you can edit and iterate on as a template for your own solution:

[Start New Project Based on Example Solution](https://bitbucket.org/osrf/servicesim/wiki/Start%20New%20Project%20Based%20on%20Example%20Solution)