# Install and run

## Installation

Installation instructions for Ubuntu Xenial (16.04)

1. Install Gazebo 8

    On a terminal, run the following commands:

        sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
        wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
        sudo apt update
        sudo apt install gazebo8 libgazebo8-dev

    Test the installation worked, run Gazebo in verbose mode, a window should
    open and version 8.X should be printed on the terminal:

        gazebo --verbose

1. Install ROS Kinetic

    On a terminal, run the following commands:

        sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
        sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
        sudo apt update
        sudo apt install -y ros-kinetic-desktop ros-kinetic-gazebo8-ros-pkgs ros-kinetic-gazebo8-ros-control
        sudo rosdep init
        rosdep update

    Test the installation worked by sourcing Kinetic and running RViz, a window
    should open:

        . /opt/ros/kinetic/setup.bash
        rosmaster & rosrun rviz rviz

1. Install ServiceSim


    A. From source

        mkdir -p ~/ws/src
        cd ws/src
        hg clone https://chapulina@bitbucket.org/osrf/servicesim
        cd ..
        . /opt/ros/kinetic/setup.sh
        rosdep install --from-paths src --ignore-src -r -y
        catkin_make

    B. From debian packages

        TODO

    Check installation worked by launching the servicesim example world:

        roslaunch servicesim servicesim.launch
