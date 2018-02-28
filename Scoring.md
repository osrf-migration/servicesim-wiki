See the [overview](https://bitbucket.org/osrf/servicesim/wiki/Checkpoints%20overview) for a summary of the checkpoints.

## Scoring

After a competition run, the competitor will receive a single number consisting of their score.

The competitor with the lowest score wins.

The final score is a weighted sum of the time to complete each checkpoint, plus penalties. The weight of each item is [configurable](https://bitbucket.org/osrf/servicesim/wiki/Scenario%20generation) in `config.yaml`.

### Checkpoint time items

* **Checkpoint 1** Time to reach pick-up location
* **Checkpoint 2** The sum of all the time intervals in which the robot took to (re)acquire the guest
* **Checkpoint 3** The sum of all the time intervals in which the guest was following the robot
* **Checkpoint 4** Time to return to start location

### Penalty items

* Collisions with office objects
* Collisions with humans
* Approximation to office objects
* Approximation to humans
* Number of failed pick-up attempts
* Number of times the guest deviated because the robot moved too fast
* Number of failed drop-off attempts

### Final score

`Score = SUM ( item_i * weight_i )`