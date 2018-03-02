# Installation

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

    ![gazebolaunch.png](https://bitbucket.org/repo/gkR8znK/images/443494770-gazebolaunch.png)

1. Install ROS Kinetic

    On a terminal, run the following commands:

        sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
        sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
        sudo apt update
        sudo apt install -y ros-kinetic-desktop ros-kinetic-gazebo8-ros-pkgs ros-kinetic-gazebo8-ros-control
        sudo rosdep init
        rosdep update
        echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
        source ~/.bashrc

    Test the installation worked by sourcing Kinetic and running RViz, a window
    should open:

        roscore & rviz

    ![rviz.png](https://bitbucket.org/repo/gkR8znK/images/3117604865-rviz.png)

    After closing the window, be sure to terminate `roscore` too, by typing:

        fg

    And then killing the program with `Ctrl + C`.
        

1. Install ServiceSim

    Install all the packages provided by ServiceSim as follows:

        sudo apt install -y ros-kinetic-servicebot*\
                            ros-kinetic-servicesim*

    Check installation worked by launching the example world:

        roslaunch servicesim servicesim.launch

    You should see 3 windows, one with the Gazebo simulation:

    ![ss1.png](https://bitbucket.org/repo/gkR8znK/images/287547113-ss1.png)

    One with sensors and other visualizations on RViz:

    ![ss2.png](https://bitbucket.org/repo/gkR8znK/images/1518887213-ss2.png)

    And an RQT dashboard with several controls and camera views:

    ![ss3.png](https://bitbucket.org/repo/gkR8znK/images/1585354643-ss3.png)

### Alternative: install from source

If you'd like to run the latest changes in the code which haven't been released yet, you can do as follows:

      mkdir -p ~/ws/src
      cd ~/ws/src
      hg clone https://bitbucket.org/osrf/servicesim
      cd ..
      rosdep install --from-paths src --ignore-src --skip-keys gazebo --skip-keys libgazebo7-dev -r -y
      catkin_make_isolated --install

Remember to source this local install for every new terminal you open, otherwise the source install can't be found.

      . ~/ws/install_isolated/setup.bash

# Updating existing installation

A. From source

    cd ~/ws/src/servicesim
    hg pull
    hg up default
    cd ../..
    . /opt/ros/kinetic/setup.sh
    rosdep install --from-paths src --ignore-src --skip-keys gazebo --skip-keys libgazebo7-dev -r -y
    catkin_make_isolated --install

B. From debian packages

    sudo apt update
    sudo apt install -y ros-kinetic-servicebot*\
                        ros-kinetic-servicesim*

## Next

Check the [Walkthrough page](https://bitbucket.org/osrf/servicesim/wiki/Walkthrough) for step-by-step instructions on how to interact with the competition