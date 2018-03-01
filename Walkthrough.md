See the [overview](https://bitbucket.org/osrf/servicesim/wiki/Checkpoints%20overview) for a summary of the checkpoints.

## Walkthrough

Let's go through a whole competition task to see how the various ROS messages and 
services listed on the
[API page](https://bitbucket.org/osrf/servicesim/wiki/API)
can be used to interact with the competition.

This tutorial will go over two different ways of interacting with the competition: via the command line or via the graphical interface. This should get competitors familiar with the competition flow.

***
### 1. Launch

Launch the competition as follows:

    roslaunch servicesim servicesim.launch

Three windows will come up: Gazebo, RViz and RQT:

![ss4.png](https://bitbucket.org/repo/gkR8znK/images/4158358454-ss4.png)

This command launches many ROS nodes at once, for more details and control on what is being launched please refer to [this page](https://bitbucket.org/osrf/servicesim/wiki/Launch%20files).

Many messages will be printed on the terminal. The ones you should look for are:

* This message confirms the competition software has been loaded:

        [Msg] [ServiceSim] Competition plugin loaded

* There is a block of text explaining how to use the keyboard teleoperation, started by:
  
        Reading from the keyboard  and Publishing to Twist!

***
### 2. Track score

The score is displayed and updated in real time on the top-right corner of the RQT window.

[Score messages](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/msg/Score.msg) are also published on the ROS topic `/servicesim/score`, so it can be tracked from a program, for example.

Using the command line, you can print score updates by running:

    rostopic echo /servicesim/score

Nothing will be printed until the task starts.

***
### 3. Start task

When you're ready to start, call the 
[new task service](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/srv/NewTask.srv)
to receive the goals for the run.

From the RQT dashboard, you can:

1. Click on the "Service Caller" refresh button
1. From the dropdown, choose `/servicesim/new_task`
1. Then click on "Call"

![ss5.png](https://bitbucket.org/repo/gkR8znK/images/2066720840-ss5.png)

Alternatively, from the command line, you can call:

    rosservice call /servicesim/new_task

The response will contain:

* The pick-up location name (i.e. `FrontDesk`, `PublicCafe`)
* The drop-off location name (i.e. `PrivateOfficeA`, `PublicMeetingRoomC`)
* The guest's identity, which matches their RFID sensor reading
* The robot's start pose in world coordinates

You'll see a message like the following on your terminal:

    [Msg] [ServiceSim] Started Checkpoint "Go to pick-up location" at 00:00:10.536
    [Msg] Started contain plugin [servicesim/go_to_pick_up]

***
### 4. Get room info

At any moment, you can use the
[room info service](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/srv/RoomInfo.srv)
to get the world coordinates of any location.

For example, if we want to know the position of the `FrontElevator` location, we can use the dashboard to call the service :

1. Choose `/servicesim/room_info` from the dropdown
1. On "Request", type the name of the location, in our case `FrontElevator`
1. Click "Call"

![ss6.png](https://bitbucket.org/repo/gkR8znK/images/1085764631-ss6.png)

Or from the command line:

    rosservice call /servicesim/room_info FrontElevator


The response will contain the XYZ world coordinates of the minimum and maximum corners of
the room's pick-up/drop-off area. See [this page](https://bitbucket.org/osrf/servicesim/wiki/Room%20names) for more details about rooms.

***
### 5. Checkpoint 1: Go to pick-up

The first checkpoint consists of navigating the robot to the pick-up location.

Once the robot has reached the correct location, you'll see the following on
the terminal:

    [Msg] Stopped contain plugin [servicesim/go_to_pick_up]
    [Msg] [ServiceSim] Checkpoint "Go to pick-up location" complete
    [Msg] [ServiceSim] Started Checkpoint "Pick-up guest" at 00:00:11.730

***
### 6. Checkpoint 2: Pick-up

For this checkpoint, it is convenient to use the RFID sensor to localize the guest. On a terminal you can listen to the sensor topic:

    rostopic echo /servicebot/rfid

Whenever the robot gets close to a person, the person's RFID identity will be notified on this topic.

When close to guest, call the 
[guest pick-up service](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/srv/PickUpGuest.srv),
for example:

    rosservice call /servicesim/pickup_guest guest servicebot

Where the first argument is the guest's name and the second one is the robot's.

If the request is successful, the guest will start following the robot.

Reasons the request could fail:

* Wrong guest name used
* Wrong robot name used
* Robot too far from guest
* Not yet on this checkpoint

If the pick-up request is successful, you'll see messages like these:

    [Msg] Actor [guest] is following model [servicebot]
    [Msg] [ServiceSim] Checkpoint "Pick-up guest" complete
    [Msg] [ServiceSim] Started Checkpoint "Drop-off guest" at 00:01:33.467

***
### 7. Checkpoint 3: Drop-off

Navigate towards the goal while making sure the guest is following.

Reasons the guest could drift away:

* Robot moved too fast and got too far from guest
* One of the random drift times defined in the world file has been reached

If the guest drifted away, you're back at **Checkpoint 2**.

Once the destination has been reached, use the
[guest drop-off service](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/srv/DropOffGuest.srv),
for example:

    rosservice call /servicesim/dropoff_guest guest

Where the argument is the guest name.

Reasons the request could fail:

* Wrong guest name used
* Guest is not in the drop-off location
* Not yet on this checkpoint

If the drop-off request is successful, you'll see this message:

    [Msg] Actor [guest] stopped following model [servicebot]
    [Msg] [ServiceSim] Checkpoint "Drop-off guest" complete
    [Msg] [ServiceSim] Started Checkpoint "Return to start" at 00:02:00.862
    [Msg] Started contain plugin [servicesim/return_to_start]

***
### 8. Checkpoint 4: Return to start

Return to the room where the robot started the competition from.

Once the robot has reached the correct location, you'll see the following on
the terminal:

    [Msg] Stopped contain plugin [servicesim/return_to_start]
    [Msg] [ServiceSim] Competition complete!


***
## Next

Check out the [programmatic tutorials](https://bitbucket.org/osrf/servicesim/wiki/Tutorials) to learn how to write a program that solves the competition.