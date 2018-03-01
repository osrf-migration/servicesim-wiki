Before we describe the contents of the solution, we'll first describe in this tutorial how you can start your own solution using our example as a template.

### Overview

In order to setup your own local working copy of our example you'll need a "[catkin workspace](http://wiki.ros.org/catkin/workspaces)" in which to build it and you'll need to download a copy of it which you can edit.

### Setting Up a Local Catkin Workspace

Before downloading our example, we'll setup a catkin workspace:

```
mkdir -p ~/my_servicesim_ws/src
```

A catkin workspace is just a folder with a prescribed layout (you can adjust the layout too, but it's recommended to go with the default).
Here we're recommending that you locate the workspace in `~/my_servicesim_ws`, but you can choose any location you like, but we do recommend sticking with a "source space" folder called `src` within the workspace.

### Downloading a Copy of the Example

Next you'll want to duplicate our package by downloading it from our source repository (the debian package you installed doesn't come with the build files you need) and making a copy of it in your local catkin workspace.

```
mkdir -p /tmp/temporary_clones
cd /tmp/temporary_clones
hg clone https://bitbucket.org/osrf/servicesim -b default
cp -r servicesim/competitor_example_solution/servicesim_example_python_solution ~/my_servicesim_ws/src
```

After that you can delete the temporary clone of our repository with

```
rm -rf /tmp/temporary_clones
```

### Renaming the example

Before making changes, you'll want to rename the package you copied to avoid confusing it with the example solution installed from `apt`.
We'll recommend that you use the new package name `my_servicesim_python_solution`, but you can pick any name you like, just make sure to use this name in the follow instructions.

First you'll want to rename the folder of the package:

```
cd ~/my_servicesim_ws/src
mv servicesim_example_python_solution my_servicesim_python_solution
```
Now open the `package.xml` file:

    gedit my_servicesim_python_solution/package.xml 

Edit it like this:

```xml
<?xml version="1.0"?>
<package format="2">
  <name>my_servicesim_python_solution</name>

  <!-- ... cut the rest of the details for brevity ->
</package>
```

Save it and close it.

Now open the `CMakeLists.txt` file:

    gedit my_servicesim_python_solution/CMakeLists.txt

And change it like this, save and close.

```cmake
cmake_minimum_required(VERSION 2.8.3)
project(my_servicesim_python_solution)

# ... cut the rest of the details for brevity
```

Finally, you need to update the launch file, so that it runs the copy of the example solution and not the one installed from `apt`:

    gedit my_servicesim_python_solution/launch/example_solution.launch 

And change:

```
<launch>
  <!-- ... cut the rest of the details for brevity -->
  <!-- the "pkg=" line is changed -->
  <node
    name="example_solution"
    pkg="my_servicesim_python_solution"
    type="example_solution.py"
    respawn="false" output="screen" />
</launch>
```

Now you're ready to build and run your copy of the example.

### Build the Copy of the Example

To build the workspace which you created above, you need to run the build command from the root directory of the workspace:

```
cd ~/my_servicesim_ws
catkin_make_isolated --install
```

### Running the copy of the example

Finally, you're ready to run your copy of the example solution.

1. On a new terminal, run the competition:

        roslaunch servicesim servicesim.launch rviz:=false teleop:=false

1. Now we're going to run your copy of the solution, which is similar to what was described in the [previous tutorial](https://bitbucket.org/osrf/servicesim/wiki/Running%20Example%20Solution). We recommend that you run things in one terminal and build things in a different terminal. So open a new terminal and then source your workspace that you built in the previous step:

        source ~/my_servicesim_ws/install_isolated/setup.bash

1. Now run your copy of the solution in that terminal:

        roslaunch my_servicesim_python_solution example_solution.launch

You can reuse the terminals to build, run the competition, and run the solution, but it's a good idea to keep a separate terminal for each task.

### Next Tutorial

In the next tutorial we will describe the contents of the example solution and point out places you might want to modify it:

[Understanding the Example Solution](http://wiki.ros.org/servicesim/Tutorials/UnderstandingTheExampleSolution)