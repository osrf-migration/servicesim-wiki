The config.yaml file contains the parameters to configure the scenario, The following are the parameters that can be modified:

## targets: ##

1. `robot_start`: This specifies the starting position of the robot, for example: `PrivateCafe`.

2. `pick_up`: This specifies the pickup location of the guest, for example: `FrontElevator`. 

3. `drop_off`: This specifies the drop-off location of the guest, for example: `PrivateCubicle_31_3` 

## guest: ##

   * `skin`: This specifies the guest's appearance. for example: `SKIN_man_blue_shirt.dae` 

## drift: ##

1. `min_interval`: This specifies the minimum time in seconds between the guest drifts, for example: `15`

2. `max_interval`: This specifies the maximum time in seconds between the guest drifts, for example: `300`

3. `count`: This specifies the total number of drifts, for example: `30`

## scoring: ##

This section specifies the various penalties and priorities that define the score when the robot performs the tasks. The weights define the severity of these penalties, for example, the weight of penalty when the robot collides with a human can be greater than the weight of penalty when the robot collides with an object. Here are the configurable weights:

1. `weight_human_contact`: This specifies the penalty weight when the robot comes in contact with a human. 

2. `weight_object_contact`: This specifies the penalty weight when the robot comes in contact with an object.

3. `weight_human_approximation`: This specifies the penalty weight when the robot comes close to a human but not touching it. 

4. `weight_object_approximation`: This specifies the penalty weight when the robot comes close to an object but not touching it.

5. `weight_pickup_location`: This specifies the weight for the time taken by the robot to reach the pickup location. 

6. `weight_pickup_guest`: This specifies the weight for the time taken by the robot to pick up the guest after reaching the pickup location.  

7. `weight_drop_off_guest`: This specifies the weight for the time taken by the robot to drop-off the guest at the drop-off location.  

8. `weight_return_start`: This specifies the weight for the time taken by the robot to go back to its start position.

9. `weight_failed_pickup`: This is a constant penalty when the guest pickup failed. 

10. `weight_failed_drop_off`: This is a constant penalty when the guest drop-off failed.  

11. `weight_too_fast`: This a constant penalty when the robot moves too fast away from the guest after it has picked up the guest. 

## humans: ##

1. `walking_count`: This specifies the number of people that are walking the office.

2. `idiling_count`: This specifies the number of people that are idle/not-walking in the office.