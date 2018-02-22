## Use the servicebot navigation stack ##

* Launch the simulation (without rviz):

    roslaunch servicesim servicesim.launch rviz:=false

* Launch the servicebot nagivation stack

    roslaunch servicebot_2dnav servicebot_move_base.launch

* Launch RViz with the navigation plugins

    roslaunch servicebot_2dnav servicebot_nav_rviz.launch

* In RViz:
 - click the "2D Nav Goal" button
 - click on the map to set a navigation goal
