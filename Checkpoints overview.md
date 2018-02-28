## Overview

When the competition starts, the robot is at a place in the map unknown in advance. The task consists of escorting a guest from a location to another in the map and then returning to the start point.

![checkpoint1.png](https://bitbucket.org/repo/gkR8znK/images/1168236894-checkpoint1.png)

***
### **Checkpoint 1** Reach guest pick-up location

The robot and the guest start in different areas of the map. See [this page](https://bitbucket.org/osrf/servicesim/wiki/Room%20names) for a list of all areas.

The first checkpoint is complete once the robot enters the same area as the guest.

***
### **Checkpoint 2** Pick-up guest

The robot needs to use its sensors and information previously provided to engage the guest and ask them to follow. Once properly engaged, the guest will start following the robot. 

While following, there is a chance that the guest stops following the robot. In that case, this checkpoint may need to be completed again. This may happen any number of times during a competition run.

***
### **Checkpoint 3** Drop-off guest

Once the robot and the guest have reached the destination area, the robot should properly inform the guest. This checkpoint is then complete. 

Note that if the guest deviates while performing **Checkpoint 3**, the robot must perform **Checkpoint 2** again (i.e. reacquire the guest). This may happen `n` times.

This only needs to be completed once per task.

***
### **Checkpoint 4** Return to start point

The robot must then return to the area where it started the competition from.

***

The following will be checked during the whole run and incur penalties:

* Colliding with objects or humans
* Getting too close to objects or humans, without necessarily colliding
* Failed attempts at picking-up or dropping-off

### More

* [Walkthrough](https://bitbucket.org/osrf/servicesim/wiki/Walkthrough) instructions
* [Scoring](https://bitbucket.org/osrf/servicesim/wiki/Scoring) details