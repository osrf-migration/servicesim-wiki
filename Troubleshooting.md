This page compiles answers to some common problems.

***
### **Q:** RQT crashes on startup

**A:** Remove RQT's ini file, running: `rm ~/.config/ros.org/rqt_gui.ini`

***
### **Q:** Error `The program 'roslaunch' is currently not installed.`

**A:** Be sure to source the ROS setup file on your `~/.bashrc` as described on the [Install page](https://bitbucket.org/osrf/servicesim/wiki/Installation), i.e.:

    echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc