## Overview

A run through the competition consists of the following checkpoints:

* **Checkpoint 1** (x 1): Reach guest pick-up location
* **Checkpoint 2** (x n): Pick-up guest
* **Checkpoint 3** (x 1): Drop-off guest
* **Checkpoint 4** (x 1): Return to starting point

Note that if the guest deviates while performing **Checkpoint 3**, the robot must perform **Checkpoint 2** again (i.e. reacquire the guest). This may happen `n` times.

The following will be checked during the whole run and incur penalties:

* Colliding with an object
* Colliding with any humans, including the guest

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

        [Msg] [ServiceSim] Started Checkpoint 1 at 00:00:05.333
        [Msg] Started contain plugin [servicesim/checkpoint1]

### Checkpoint 1

The first checkpoint consists of navigating the robot to pick-up location.

Once the robot has reached the correct location, you'll see the following on
the terminal:

    [Msg] Stopped contain plugin [servicesim/checkpoint1]
    [Msg] [ServiceSim] Checkpoint [1] complete

### Checkpoint 2

When close to guest, call the `PickUpGuest` service, for example:

    rosservice call /servicesim/pickup_guest guest servicebot

Where the first argument is the guest's name and the second one is the robot's.

If the request is successful, the guest will follow the robot.

Reasons the request could fail:

* Wrong guest name used
* Wrong robot name used
* Robot too far from guest

### Checkpoint 3

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

### Checkpoint 4

Return to the point where the robot started the competition from.