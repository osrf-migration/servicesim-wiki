The [config.yaml](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/worlds/config.yaml) file contains parameters to configure a unique competition scenario.

The following are the parameters that can be modified. Parameters left empty will be randomized unless a default value is specified.

## targets ##

Target configuration. See the [full list](https://bitbucket.org/osrf/servicesim/wiki/Room%20names) of location names.

* `pick_up`: The pick-up location of the guest, for example: `FrontElevator`. 

* `drop_off`: The drop-off location of the guest, for example: `PrivateCubicle_31_3` 

* `robot_start`: The starting location of the robot, for example: `PrivateCafe`.

* `robot_start_yaw`: The starting yaw of the robot (zero is looking at +X)

## guest ##

Configurations of the guest to be picked up.

* `skin`: The guest's appearance, which is a `SKIN` file from [here](https://bitbucket.org/osrf/servicesim/src/default/servicesim_competition/models/actor/meshes/), for example: `SKIN_man_blue_shirt.dae` 

## drift ##

Parameters used to randomly generate guest drift times

* `min_interval`: The minimum time in seconds between the guest drifts for example: `15`

* `max_interval`: The maximum time in seconds between the guest drifts for example: `300`

* `start_time`: Before this time (in seconds), no drifts are generated

* `count`: The total number of drifts, for example: `30`

## scoring ##

See the [Scoring page](https://bitbucket.org/osrf/servicesim/wiki/Scoring) for more details on scoring.

This section specifies the various penalties and priorities that define the score when the robot performs the tasks. The weights define the severity of these penalties, for example, the weight of the penalty when the robot collides with a human can be greater than the weight of the penalty when the robot collides with an object. Here are the configurable weights:

* `weight_human_contact`: The penalty weight when the robot comes in contact with a human. 

* `weight_object_contact`: The penalty weight when the robot comes in contact with an object.

* `weight_human_approximation`: The penalty weight when the robot comes close to a human but not touching it. 

* `weight_object_approximation`: The penalty weight when the robot comes close to an object but not touching it.

* `weight_pickup_location`: The weight for the time taken by the robot to reach the pickup location. 

* `weight_pickup_guest`: The weight for the time taken by the robot to pick up the guest after reaching the pickup location.  

* `weight_drop_off_guest`: The weight for the time taken by the robot to drop-off the guest at the drop-off location.  

* `weight_return_start`: The weight for the time taken by the robot to go back to its start position.

* `weight_failed_pickup`: This is a constant penalty when the guest pickup failed. 

* `weight_failed_drop_off`: This is a constant penalty when the guest drop-off failed.  

* `weight_too_fast`: This a constant penalty when the robot moves too fast away from the guest after it has picked up the guest. 

## humans ##

* `walking_count`: The number of people that are walking in the office.

* `idiling_count`: The number of people that are idle/not-walking in the office.