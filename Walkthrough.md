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

You should also see that the score starts increasing.

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

The first checkpoint consists of navigating the robot to the pick-up location. In our case, this is the `FrontElevator`.

For this walkthrough, there are a few ways you can move the robot there:

#### A. Using the keyboard teleoperation

1. Click on the terminal from which you ran `roslaunch` to make sure it has focus
1. Use the keyboard as described on the terminal to steer the robot around the world

#### B. Using the RQT dashboard

You can use the "Robot Steering" widget to control the robot:

![ss7.png](https://bitbucket.org/repo/gkR8znK/images/1388713375-ss7.png)

#### C. Moving the robot on Gazebo

For quick testing, you could also use the translation tool on Gazebo to teleport the robot to the `FrontElevator` area:

![ss8.gif](https://bitbucket.org/repo/gkR8znK/images/986763748-ss8.gif)

Once the robot has reached the correct location, you'll see the following on
the terminal:

    [Msg] [ServiceSim] Checkpoint "Go to pick-up location" complete
    [Msg] [ServiceSim] Started Checkpoint "Pick-up guest" at 00:00:11.730

***
### 6. Use the RFID sensor

For the next checkpoint, it will be convenient to use the robot's RFID sensor to localize the guest. On a terminal you can listen to [RFID sensor messages](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/msg/ActorNames.msg):

    rostopic echo /servicebot/rfid

Whenever the robot gets close to a person, the person's RFID identity will be notified on this topic, for example:

~~~
$ rostopic echo /servicebot/rfid
actor_names: ['human_24182', 'human_86138']
---
actor_names: ['human_24182', 'human_86138']
---
actor_names: ['human_24182', 'human_86138']
---
actor_names: ['human_24182', 'human_86138']
~~~

***
### 7. Checkpoint 2: Pick-up guest

Once you've made sure you're close to the guest, call the 
[guest pick-up service](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/srv/PickUpGuest.srv),
for example:

    rosservice call /servicesim/pickup_guest human_86138 servicebot

Where the first argument is the guest's name and the second one is the robot's. This is simulating a real-world interaction in which the robot would engage the human guest.

You can also call this service from the dashboard's "Service Caller".

If the request is successful, the guest will start following the robot.

There are a few reasons the request could fail, which will be printed on the terminal if it happens and result in a score penalty. These are:

* Wrong guest name used
* Wrong robot name used
* Robot too far from guest
* Not yet on this checkpoint

If the pick-up request is successful, you'll see messages like these:

    [Msg] [ServiceSim] Checkpoint "Pick-up guest" complete
    [Msg] [ServiceSim] Started Checkpoint "Drop-off guest" at 00:01:33.467

***
### 8. Checkpoint 3: Drop-off

Navigate towards the goal while monitoring the guest to make sure they are following. You can also try this out by teleoperating the robot or teleporting it on simulation.

The competition makes the human drift away from the robot from time to time. When that happens, the competitor is back at **Checkpoint 2** and must navigate back towards the guest and call the pick-up service once more.

The guest could also drift away because the robot moved too fast for them to follow, this incurs a penalty.

Once the destination has been reached, use the
[guest drop-off service](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/srv/DropOffGuest.srv),
for example:

    rosservice call /servicesim/dropoff_guest guest

Where the argument is the guest name.

Reasons the request could fail:

* Wrong guest name used
* Guest is not in the drop-off location (make sure the guest themselves are inside the min/max coordinates given by the  `room_info` service)
* Not yet on this checkpoint

If the drop-off request is successful, you'll see this message:

    [Msg] [ServiceSim] Checkpoint "Drop-off guest" complete
    [Msg] [ServiceSim] Started Checkpoint "Return to start" at 00:02:00.862

***
### 9. Checkpoint 4: Return to start

The last checkpoint consists of returning to the room where the robot started the competition from.

Once the robot has reached the correct location, you'll see the following on
the terminal:

    [Msg] [ServiceSim] Competition complete!


***
## Next

Check out the [programmatic tutorials](https://bitbucket.org/osrf/servicesim/wiki/Tutorials) to learn how to write a program that solves the competition.