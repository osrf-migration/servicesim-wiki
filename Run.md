1. Request guest identity / location / destination

    TODO

1. Approach guest

1. When close to guest, call the `PickUpGuest` service, for example:

        rosservice call /servicesim/pickup_guest guest servicebot

    Where the first argument is the guest's name and the second one is the robot's.

    If the request is successful, the guest will follow the robot.

    Reasons the request could fail:

    * Wrong guest name used
    * Wrong robot name used
    * Robot too far from guest

1. Navigate towards the goal while making sure the guest is following.

    Reasons the guest could drift away:

    * Robot moved too fast and got too far from guest
    * One of the random drift times defined in the world file has been reached

1. If the guest drifted away, go back to step 2

1. Once the destination has been reached, use the `DropOffGuest` service, for example:

        rosservice call /servicesim/dropoff_guest guest

    Where the argument is the guest name.

    Reasons the request could fail:

    * Wrong guest name used