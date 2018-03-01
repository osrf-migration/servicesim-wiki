ServiceSim comes with an example solution to the competition to illustrate how to use the ROS interfaces and how you could structure your own solution.

This tutorial will show you how to run the example and explain the code within the example.

### Prerequisites

Before doing this tutorial you need to have installed `servicesim` from the debian files via `apt`, as described on the [Installation Page](https://bitbucket.org/osrf/servicesim/wiki/Installation).

### Running the Competition

Before running the solution, we need to start the competition:

    roslaunch servicesim servicesim.launch rviz:=false teleop:=false

This will launch `gazebo` and the `rqt` dashboard, but it prevents the keyboard teleoperation from starting (since we'll be controlling autonomously), as well as preventing `rviz` from starting since our example solution has a different `rviz` configuration which is displays more relevant information related to the navigation stack used by our example.

### Running the Example Solution

Once the competition software has started, we can run the example competition solution in a separate terminal:

    roslaunch servicesim_example_python_solution example_solution.launch

This will run a few things:

- the [ROS navigation stack](http://wiki.ros.org/navigation), which we use to autonomously navigate the robot
- RViz with a custom display configuration
- the example solution, `example_solution.py`, which we'll go over in detail later

### Observe the Solution

![ss11_opt.gif](https://bitbucket.org/repo/gkR8znK/images/643991455-ss11_opt.gif)

While the solution is running, you can observe the robot and humans moving in the Gazebo simulation.

On RViz, you will see what the navigation stack is computing over time. There are the local and global cost maps, pose, plan and cost cloud.

On the terminal, you can see updates printed by the state machine as it progresses through the competition, such as its current state, the RFID sensor readins and so on, for example:

~~~
[INFO] [1519942333.781666, 8.236000]: In Pickup state
[INFO] [1519942333.782325, 8.236000]: clearing costmaps
[INFO] [1519942335.170250, 8.746000]: sent goal
[INFO] [1519942361.150206, 17.802000]: ['human_88042']
[INFO] [1519942363.802807, 18.746000]: action timed out in state: 1
...
[INFO] [1519942564.762658, 87.654000]: requesting follow
[INFO] [1519942564.766809, 87.656000]: success: True
[INFO] [1519942564.767655, 87.658000]: In DropOff state
...
~~~

### Next Tutorial

The next tutorial will describe how you can get a local working copy of our example solution which you can edit and iterate on as a template for your own solution:

[Start New Project Based on Example Solution](https://bitbucket.org/osrf/servicesim/wiki/Start%20New%20Project%20Based%20on%20Example%20Solution)