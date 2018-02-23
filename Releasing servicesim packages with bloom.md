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

### Triggering new package builds

From the [servicesim project](https://build.osrfoundation.org/view/proj_servicesim/) the buildfarm.
Trigger new builds of the packaging jobs, which all end in `-bloom-debbuilder`. There are two _required_ parameters that must be set.

* `VERSION`: The package version to build. Right now we're on version `0.0.0` but that could change.
* `RELEASE_VERSION`: This is also referred to as a deb increment. This indicates a change in the package but not a change in the source.

Both of these variables can be extracted from bloom's running output. As an example if you see the output below

```
####
#### Successfully generated 'xenial' debian for package 'servicebot_description' at version '0.0.0-3'
####
```

then the `VERSION` is `0.0.0` and the `RELEASE_VERSION` is `3`.

***NOTE:*** If any packages have build dependencies on their siblings (other servicesim project packages), make sure the builds for dependent packages are not triggered until the dependency builds successfully and is uploaded to the repository.

## Adding a new servicesim package

If a new package is added to the servicesim project, a new bloom release must be made and a packaging job must be created for it.

1. Run bloom (as above) and the new package will be automatically detected.
2. Add the name of the package to the [list in release-tools](https://bitbucket.org/osrf/release-tools/src/1f2b2c01e3d09e23cfbe1617de22b2bbec589edb/jenkins-scripts/dsl/servicesim.dsl?at=default&fileviewer=file-view-default#servicesim.dsl-9).
3. Trigger a new build of https://build.osrfoundation.org/view/proj_servicesim/job/_dsl_servicesim/
3. Trigger new builds for all servicesim packages (as above).