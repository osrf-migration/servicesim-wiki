## Use the ServiceBot navigation stack

1. If you haven't done so already, launch the simulation. We can set `rviz` to false because we will be opening a new window, and `teleop` to false because we won't be teleoperating the robot:

        roslaunch servicesim servicesim.launch rviz:=false teleop:=false

1. Launch the servicebot navigation stack

        roslaunch servicebot_2dnav servicebot_move_base.launch

1. Launch RViz with the navigation plugins

        roslaunch servicebot_2dnav servicebot_nav_rviz.launch

    A new window will open with the navigation map.

    ![rviznav.png](https://bitbucket.org/repo/gkR8znK/images/3521375243-rviznav.png)

1. When the navigation starts, the robot doesn't have a good idea about where it is. You can see on the image above how it thinks it is near the private cafe. The first thing we need to do is to give the robot a rough estimate of where it is. To do that:

    1. Click on `2D Pose Estimate`
    1. Press the mouse on a point on the map near where the robot is (a green arrow will appear)
    1. Move the mouse towards the direction the robot is facing (the green arrow will rotate)
    1. Release the mouse button - the robot's sensor readings will start matching the map

        ![poseestimate.gif](https://bitbucket.org/repo/gkR8znK/images/3150653352-poseestimate.gif)

1. Now the robot is ready to receive navigation goals:

    1. Click on `2D Nav Goal`
    1. The same way as before, press, move and release the mouse to set a target
    1. Observe the robot navigating towards that point

        ![goal_opt.gif](https://bitbucket.org/repo/gkR8znK/images/1423354261-goal_opt.gif)