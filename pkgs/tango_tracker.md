---
title: tango-tracker
layout: repository
---

## Package overview  

Contains nodes for tracking an ARUCO marker which publish it's orientation and position.

Expects ARUCO markers of the 5X5_50 type.

## Nodes

---

### tango_tracker.py  

Tracks an ARUCO marker using image frames from a realsense depth camera. calculating the ARUCO marker's orientation and the position of it's centre.

Also calculates the pixel to meters scale of the image using the expected size of the ARUCO marker.

#### Info

Default node name: *tango_tracker*

Dependencies: *rospy, sensor_msgs, geometry_msgs, std_msgs, cv_bridge, cv2, imutils*

ROS Rate: *7hz*

#### Topics

##### Subscribes

- */camera/color/image_raw* (sensor_msgs/Image): Images from camera which may contain an ARUCO marker.

##### Publishes
  
- */position_2d* (geometry_msgs/Point): Pixel position of the centre of the ARUCO marker.

- */orientation_2d* (std_msgs/Int16): Orientation of the ARUCO marker in degrees from the Y axis.

- */px_scale* (std_msgs/Float32): Pixel to meters scale calculated from the expected size in cm of the ARUCO marker.

- */debug/final_img* (sensor_msgs/Image): Image from the camera with debug information drawn on.

#### Parameters

- *~marker_size* (float): Width/Height in centimeters of the ARUCO marker (these two values should be the same).

- *~show_ui* (bool): Show the realtime debug images using opencv2 UI. Defaults to False.

- *~robot_arucoID* (int): The ID of the ARUCO marker which should be tracked. If -1, data for the lowest ID present will be output. Defaults to -1.

- *~debug_video* (bool): Output the debug frames as a video when node shutsdown. Defaults to False.

- *~video_location* (str): Location to output the debug video to. Should be of the filetype '.AVI'. Defaults to '~/DebugVideo.avi'.

## Launch files

### tracker_debug

Test the tango_tracker node with a rosbag.

#### Info

Dependency Packages: *none*

Usage: ```roslaunch tango_tracker tracker_debug.launch rosbag_path:=[PATH_TO_ROS_BAG] marker_size:=[MARKER_WIDTH]```

#### Arguments

- *rosbag_path* (str): Path to a rosbag containing camera image topic.

- *marker_size* (float): Width/Height in centimeters of the ARUCO marker.

### tracker_isl

Test the tango_tracker with realtime camera frames.

#### Info

Dependency Packages: *realsense2_camera*

Usage: ```roslaunch tango_tracker tracker_isl.launch marker_size:=[MARKER_WIDTH]```

#### Arguments

- *marker_size* (float): Width/Height in centimeters of the ARUCO marker.

For a full list of arguments for the camera settings, see the tracker_isl file and the realsense2_camera package documentation.