# tango_rtabmap
ROS package using rtabmap and move_base to construct a map from sensor data in real time to be used in path planning and navigation applications.
Configured for the tango robot

## Setup:
Place the contents of this repository in the directory:
```<path_worksapce_dir>/src/tango_rtabmap```

Make sure you have all required dependancies already installed: \[Ubuntu]
- Tango software stack, available [**<ins>here</ins>**](https://github.com/fearn-robotics)
- ```sudo apt install ros-noetic-move-base```
- ```sudo apt install ros-noetic-rtabmap-ros```
- ```sudo apt install ros-noetic-global-planner```
- ```sudo apt install chrony```
- DWA planner causes std::badalloc() errors if installed via apt, please install from source [**<ins>here</ins>**](https://github.com/ros-planning/navigation/tree/noetic-devel/dwa_local_planner)

Build and source your ROS workspace:
- ```cd <path_to_workspace_dir>```
- ```catkin_make```
- ```source devel/setup.bash```

## Arguments
```use_bag``` (Bool) - Default = false - Enables the running of a rosbag for simulated testing of internal systems

```use_rviz``` (Bool) - Default = true - Enables visualization

```use_nav``` (Bool) - Default = true - Enables the move_base navigation component

```bag``` (String) - Default = "/home/tango/datasets/2022-06-06-14-05-29.bag" - full path to bag if required

## Current usage:
This package contains the required launch and parameter files to construct a navigatable map from either live data, or a rosbag, with said data being the contents of ```/odom``` and ```/scan``` topics. In future, this package could be configured to work with a saved map (.db), map server and localization script lib (amcl).

These systems together provide the functionality to enable real world path planning and navigation systems.

By default, the system is configured to run with both vizualization and navigation functionality enabled and bags disabled, for real world usage.
Arguments are provided for simulated usage with rosbags and the ability to disable visualization and move_base compatibilty for testing and interoperabilty reasons.

### Default command usage:
```roslaunch tango_rtabmap tango_rtabmap_start.launch```

### Running with bag enabled:
```roslaunch tango_rtabmap tango_rtabmap_start.launch use_bag:=true bag:=<path_to_bagfile>/<filename>.bag```

### Running just mapping:
```roslaunch tango_rtabmap tango_rtabmap_start.launch use_rviz:=false use_nav:=false```
