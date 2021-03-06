# Using a different robot

This page explains how to use a robot other than ServiceBot in ServiceSim.

1. Build ServiceSim from source

    Follow the install from source instructions on the [Installation page](Installation.md).

1. Choose a robot

    Choose the robot you want to use, in our example we'll use the Segway RMP210.

    Make sure the robot you choose has a URDF description package, in our case, it is located here:

    https://github.com/StanleyInnovation/segway_v3/tree/master/segway_description

1. Install the robot description

    For simplicity, let's add the robot description into the ServiceSim
    workspace so everything can be installed with the same command:

        cd ~/ws/src
        git clone https://github.com/StanleyInnovation/segway_v3
        cd segway_v3
        rm -rf !(segway_description)
        cd ../..
        catkin_make_isolated --install

    Take a look at the description package's `launch` directory. There should be a `.launch`
    file there which, at a minimum, sets the `robot_description` parameter. I our case,
    that is:

        src/segway_v3/segway_description/launch/description.launch

1. Create a new competition launch file

    Create a new `servicesim_segway.launch` file:

        gedit src/servicesim/servicesim/launch/servicesim_segway.launch

    And put the following contents:

        <launch>

          <arg name="robot" default="true" />
          <arg name="custom" default="false" />
          <arg name="custom_prefix" default="" />

          <include file="$(find segway_description)/launch/description.launch" />

          <include file="$(find servicesim_competition)/launch/competition.launch">
            <arg name="custom" value="$(arg custom)"/>
            <arg name="custom_prefix" value="$(arg custom_prefix)"/>
          </include>

          <group if="$(arg robot)">
            <arg if="$(arg custom)" name="launch_file" default="$(arg custom_prefix).launch" />
            <arg unless="$(arg custom)" name="launch_file" value="$(find servicesim)/launch/spawn_urdf.launch"/>
            <include file="$(arg launch_file)" />
          </group>

        </launch>

    This will:

    * Launch Gazebo running the competition software
    * Launch the `segway_description` file
    * Spawn the `segway` model into the world

    This will not:

    * Launch any controllers for the robot
    * Work with the example solution

1. Install and run

    Build and install as usual:

        catkin_make_isolated --install

    Launch the new competition file:

        roslaunch servicesim servicesim_segway.launch

    You'll see the Segway inside the competition instead of ServiceBot:

    ![segway2.png](https://bitbucket.org/repo/gkR8znK/images/2528540155-segway2.png)

    The Segway meshes don't have nice textures, so we can turn on transparency
    and joint visuals to inspect that it was correctly loaded:

    ![segway1.png](https://bitbucket.org/repo/gkR8znK/images/1039098822-segway1.png)

1. Test the competition

    You can follow the instructions on the [Walkthrough page](Walkthrough.md) and check
    that the competition logic is working.

    Since this example doesn't load any controllers for the robot, this can be tested
    in "god mode" by teleporting the robot inside Gazebo.

    Try using the command line to ask for a new task, pick-up and drop the guest.

1. (Optional) Change robot name

    You can see that the Segway is called `servicebot` in the simulation. If it's
    desired to change the robot's name, you can change the `robot: name` property
    on the `config.yaml` file and then generate a custom scenario as described on
    the [Scenario generation page](Scenario generation.md).