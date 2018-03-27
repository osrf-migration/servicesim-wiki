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

On the terminal, you can see updates printed by the state machine as it progresses through the competition, such as its current state, the RFID sensor readings and so on, for example:

~~~
[INFO] [1522186485.100795, 27.102000]: -- State: Pickup
[INFO] [1522186487.307609, 27.626000]: Sent pick-up goal
[INFO] [1522186508.582517, 31.902000]: ['human_94763', 'human_80283']
[INFO] [1522186517.008667, 33.626000]: Action failed in state: 1
...
[INFO] [1522186745.655162, 72.314000]: Requesting follow
[INFO] [1522186745.665678, 72.316000]: success: True
[INFO] [1522186745.666600, 72.316000]: -- State: DropOff
[INFO] [1522186752.294614, 73.300000]: ['human_32907', 'human_20843']
...
~~~

#### Re-acquiring guest after drift

The solution will also re-pick-up the guest in case the guest drifts away while following
the robot. In case you don't want to wait for the guest to randomly drift, you can use the
[Drift service](https://bitbucket.org/osrf/servicesim/src/c67db943076feaa46cde8b594de1172ee4db7f9b/servicesim_competition/srv/Drift.srv) to trigger an immediate drift as follows:

    rosservice call /servicesim/drift

Then:

1. The robot will keep moving until the guest's RFID sensor is out of range.
1. ServiceBot will then start rotating to the left looking for the guest.
1. You can choose on the dashboard to see the image on the `/servicebot/bbox_distance`
   topic to see the robot's front-camera image with 4 dots delimiting the guest's bounding box.
1. Once the bounding box is in the center of the robot's view, the robot will go to the guest
   and pick them up again.

![repickup.gif](https://bitbucket.org/repo/gkR8znK/images/1527883351-repickup.gif)


### Next Tutorial

The next tutorial will describe how you can get a local working copy of our example solution which you can edit and iterate on as a template for your own solution:

[Start New Project Based on Example Solution](https://bitbucket.org/osrf/servicesim/wiki/Start%20New%20Project%20Based%20on%20Example%20Solution)