ServiceSim comes with an example image processing node for the competitor to modify and integrate in their solution to the competition.

This tutorial will show you how to run the example and explain the code within the example.

### Prerequisites

Before doing this tutorial you need to have installed `servicesim` from the debian files via `apt`, as described on the [Installation Page](https://bitbucket.org/osrf/servicesim/wiki/Installation).

### Running the Competition

Before running the solution, we need to start the competition:

    roslaunch servicesim servicesim.launch rviz:=false teleop:=false

This will launch `gazebo` and the `rqt` dashboard, but it prevents the keyboard teleoperation from starting (since we'll be controlling autonomously), as well as preventing `rviz` from starting since our example solution has a different `rviz` configuration which is displays more relevant information related to the navigation stack used by our example.

### Running the Example Solution

Once the competition software has started, we can run the example competition solution in a separate terminal:

    rosrun servicesim_example_python_solution image_processing_example.py

### Observe the Solution

While the solution is running, you can use the dashboard to observe the image the robot camera sends and the processed image. To do so you can hit the refresh button and select the `/servicebot/camera_front/segmented_image` topic in the drop down list of the image viewer.
![select_segmented.png](https://bitbucket.org/repo/gkR8znK/images/2203909894-select_segmented.png)

We can now visualize the results:

![blue_pixels_only_cropped.png](https://bitbucket.org/repo/gkR8znK/images/3803119328-blue_pixels_only_cropped.png)

### Next Tutorial

The next tutorial will dive into the code of this demo and how it can be extended:

[Understanding Image Processing Example](http://wiki.ros.org/servicesim/Tutorials/UnderstandingTheImageProcessingExample)