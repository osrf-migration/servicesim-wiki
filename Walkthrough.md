See the [overview](https://bitbucket.org/osrf/servicesim/wiki/Checkpoints%20overview) for a summary of the checkpoints.

## Walkthrough

Let's go through a whole competition task to see how the various ROS messages and 
services listed on the
[API](https://bitbucket.org/osrf/servicesim/wiki/API)
can be used to interact with the competition.

We'll be using the command line to trigger ROS services and listen to messages, but
during the competition, these should be done programatically.

> **Tip**: Don't forget to source the appropriate setup files for every new terminal

### Start

1. Launch the competition:

        roslaunch servicesim servicesim.launch

    This launchfiles launch many nodes at once, for more details and control on what is being launch please refer to
[this page](https://bitbucket.org/osrf/servicesim/wiki/Servicesim_Launchfiles)

    On your terminal you should see, among other messages, this one:

        [Msg] [ServiceSim] Competition plugin loaded

1. Start listening to 
[score messages](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/msg/Score.msg).
On a new terminal, run:

        rostopic echo /servicesim/score

    Nothing will be printed until the task starts.

1. When you're ready to start, call the 
[new task service](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/srv/NewTask.srv)
to receive the goals for the run:

        rosservice call /servicesim/new_task

    The response will contain:

    * The guest's identity, which will match their RFID sensor reading
    * The pick-up location name (i.e. `FrontDesk`, `PublicCafe`)
    * The drop-off location name (i.e. `PrivateOfficeA`, `PublicMeetingRoomC`)

    You'll see a message like the following on your terminal:

        [Msg] [ServiceSim] Started Checkpoint "Go to pick-up location" at 00:00:10.536
        [Msg] Started contain plugin [servicesim/go_to_pick_up]

1. At any moment, you can use the
[room info service](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/srv/RoomInfo.srv)
to get the world coordinates of any location.
For example, if we want to know the position of room `PrivateCafe`, we can call:

        rosservice call /servicesim/room_info PrivateCafe

    The response will contain the XYZ world coordinates of the minimum and maximum corners of
the room's pick-up/drop-off area. According to the room, this may be inside or in front of
it. For example, a meeting room's area is inside it, but a bathroom's area is in front of it.
All rooms have rectangular areas which are aligned with the world.

### Checkpoint 1: Go to pick-up

The first checkpoint consists of navigating the robot to the pick-up location.

Once the robot has reached the correct location, you'll see the following on
the terminal:

    [Msg] Stopped contain plugin [servicesim/go_to_pick_up]
    [Msg] [ServiceSim] Checkpoint "Go to pick-up location" complete
    [Msg] [ServiceSim] Started Checkpoint "Pick-up guest" at 00:00:11.730

### Checkpoint 2: Pick-up

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

### Checkpoint 3: Drop-off

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

### Checkpoint 4: Return to start

Return to the room where the robot started the competition from.

Once the robot has reached the correct location, you'll see the following on
the terminal:

    [Msg] Stopped contain plugin [servicesim/return_to_start]
    [Msg] [ServiceSim] Competition complete!