# Prerequisites

* Bloom >= 0.6.0
* git
* rosdep

```
#!bash
# or python3-{bloom,rosdep} to use python 3. Both work.
apt-get install git python-bloom python-rosdep
```

### Set rosdep keys for gazebo8 ###

```
#!bash
sudo wget https://raw.githubusercontent.com/osrf/osrf-rosdep/master/gazebo8/00-gazebo8.list -O /etc/ros/rosdep/sources.list.d/00-gazebo8.list
rosdep update
```

# Creating a new release

Clone the release repository or update an existing clone and run the `git bloom-release $TRACK` command.
Right now the only track is `default` which tracks the tip of the default servicesim branch.

```
#!bash
git clone https://bitbucket.org/osrf/servicesim-release # Depending on your setup an ssh clone might be preferred.
cd servicesim-release
git bloom-release default
```

If bloom runs successfully it will suggest that you run

```
#!bash
git push --all && git push --tags
```