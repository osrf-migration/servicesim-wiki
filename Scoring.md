See the [overview](https://bitbucket.org/osrf/servicesim/wiki/Checkpoints%20overview) for a summary of the checkpoints.

## Scoring

After a competition run, the competitor will receive a single number consisting of their score.

The competitor with the lowest score wins.

The final score is a weighted sum of the time to complete each checkpoint, plus penalties. The weight of each item is configurable in `service.world`.

Checkpoint time items:

* Time to reach pick-up location (CP1)
* The sum of all the times the robot took to re-acquire the guest (CP2)
* The sum of all the times the guest was following the robot (CP3) 
* Time to return to start location (CP4)

Penalty items:

* Number of collisions with office objects
* Number of collisions with humans
* Number of collisions with guest
* Number of failed pick-up attempts

So the final score is:

`Score = SUM ( item_i * weight_i )`