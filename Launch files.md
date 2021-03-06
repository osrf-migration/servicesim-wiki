## Launchfiles details

The servicesim package provides an entrypoint launchfile called `servicesim.launch`

This launchfile will start several nodes useful for the competition:

* Gazebo with the competition world and the robot
* Rviz with the robot model and the LIDAR visualization (argument `rviz`)
* A teleop node to be able to drive the robot with the keyboard (argument `teleop`)
* The ROS controllers to command the robot's head joints (argument `controllers`)
* An rqt window displaying the 2 cameras, current score in the competition, sliders that enable the control of head joints, sliders that enable to drive the robot (can also use `W` `A` `S` `D` and `space` keys from the keyboard to drive the robot from rqt window) and a service window to call the various competition services (argument `dashboard`)


Each of these parts can be enabled or disabled independently using arguments. For example to launch everything but rviz you can run:

    roslaunch servicesim servicesim.launch rviz:=false

You can also launch each of these nodes individually by using their individual launchfiles.
To launch the rviz node separately you can run:

    roslaunch servicesim rviz.launch

To launch the head controllers separately you can run:

    roslaunch servicebot_control servicebot_control.launch