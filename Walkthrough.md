See the [overview](https://bitbucket.org/osrf/servicesim/wiki/Checkpoints%20overview) for a summary of the checkpoints.

## Walkthrough

### Start

1. Launch the competition:

        roslaunch servicesim servicesim.launch

    On your terminal you should see, among other messages, this one:

        [Msg] [ServiceSim] Competition plugin loaded

1. When you're ready to start, call the new task service to receive the
goals for the run:

        rosservice call /servicesim/new_task

    The response will contain (exact format is TBD):

    * The guest's identity
    * The pick-up location
    * The drop-off location

    You'll see a message like the following on your terminal:

        [Msg] [ServiceSim] Started Checkpoint "Go to pick-up location" at 00:00:10.536
        [Msg] Started contain plugin [servicesim/go_to_pick_up]

### Checkpoint 1: Go to pick-up

The first checkpoint consists of navigating the robot to the pick-up location.

Once the robot has reached the correct location, you'll see the following on
the terminal:

    [Msg] Stopped contain plugin [servicesim/go_to_pick_up]
    [Msg] [ServiceSim] Checkpoint "Go to pick-up location" complete
    [Msg] [ServiceSim] Started Checkpoint "Pick-up guest" at 00:00:11.730

### Checkpoint 2: Pick-up

When close to guest, call the `PickUpGuest` service, for example:

    rosservice call /servicesim/pickup_guest guest servicebot

Where the first argument is the guest's name and the second one is the robot's.

If the request is successful, the guest will follow the robot.

Reasons the request could fail:

* Wrong guest name used
* Wrong robot name used
* Robot too far from guest

If the pick-up request is successful, you'll see this message:

    [Msg] Actor [guest] is following model [servicebot]
    [Msg] [ServiceSim] Checkpoint "Pick-up guest" complete
    [Msg] [ServiceSim] Started Checkpoint "Drop-off guest" at 00:01:33.467

### Checkpoint 3: Drop-off

Navigate towards the goal while making sure the guest is following.

Reasons the guest could drift away:

* Robot moved too fast and got too far from guest
* One of the random drift times defined in the world file has been reached

If the guest drifted away, you're back at **Checkpoint 2**.

Once the destination has been reached, use the `DropOffGuest` service, for example:

    rosservice call /servicesim/dropoff_guest guest

Where the argument is the guest name.

Reasons the request could fail:

* Wrong guest name used
* Wrong drop-off location

If the drop-off request is successful, you'll see this message:

    [Msg] Actor [guest] stopped following model [servicebot]
    [Msg] [ServiceSim] Checkpoint "Drop-off guest" complete
    [Msg] [ServiceSim] Started Checkpoint "Return to start" at 00:02:00.862

### Checkpoint 4: Return to start

Return to the point where the robot started the competition from.