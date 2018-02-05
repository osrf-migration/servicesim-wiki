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
* A failed attempt at pick-up or drop-off

### More

* [Walkthrough](https://bitbucket.org/osrf/servicesim/wiki/Walkthrough) instructions
* [Scoring](https://bitbucket.org/osrf/servicesim/wiki/Scoring) details