---
title: translate_coords
layout: repository
---

## Package overview  

The translate_coords package contains nodes for converting pixel coordinates from an overhead depth camera to movebase goals intended for a mobile robot.

## Nodes

---

### cam_to_depthcoords.py  

Deprojects pixel coordinates from an overhead depth camera into 3D points in the camera coordinate system, measured in meters.

The 3D points are XYZ coordinates with X being the horizontal distance to the camera side to side, Y being the horizontal distance up and down, and Z being the vertical distance. Note that this coordinate system follows the Left Hand Rule.

#### Info

Default node name: *cam_to_depthcoords*

Dependencies: *rospy, ros_numpy, cv_bridge, geometry_msgs, sensor_msgs, numpy, pyrealsense2*

ROS Rate: *30hz*

#### Topics

##### Subscribes

- */camera/depth/camera_info* (sensor_msgs/CameraInfo): The intrinsic parameters from the overhead camera.

- */camera/aligned_depth_to_color/image_raw* (sensor_msgs/CameraInfo): The depth image frames from the overhead camera.

- *input_coords* (geometry_msgs/Point): The 2D coordinates to deproject into 3D points.

##### Publishes
  
- *depth_coords* (geometry_msgs/Point): The deprojected 3D points, measured in meters.

---

### cam_transform.py

Broadcasts a static transform from the map frame to the camera base frame.  

#### Info

Default node name: *cam_tf_broadcaster*

Dependencies: *rospy, tf2, geometry_msgs*

ROS Rate: *none*

#### Parameters

- *~tf_pos* ([float, float, float]): XYZ translation for transform. Defaults to [0, 0, 0].
- *~tf_rot* ([float, float, float, float]): Quaternion rotation for transform. Defaults to [0, 0, 0, 0].
- *~map_frame* (string): Name of map frame. Defaults to 'map'.
- *~cam_frame* (string): Name of camera frame. Defaults to '_link'.
  
---

### depth_to_mapcoords.py

Transforms 3D points in the camera coordinate system to the map frame.

It should be noted that ROS coordinates follow the Right Hand Rule whilst the camera coordinate system follows the Left Hand Rule, so the Z axis of the input points are flipped to account for this.

A transform between the camera frame and the map frame must be broadcast before this node starts, for example by starting the *cam_transform* node.

#### Info

Default node name: *depth_to_mapcoords*

Dependencies: *rospy, tf2_ros, geometry_msgs, tf2_geometry_msgs*

ROS Rate: *30hz*

#### Topics

##### Subscribes

- *depth_coords* (geometry_msgs/Point): The camera 3D points to translate.

##### Publishes
  
- *realworld_coords* (geometry_msgs/PointStamped): The translated points, now in the map frame.

#### Parameters

- *~map_frame* (string): Name of map frame. Defaults to 'map'.
- *~cam_frame* (string): Name of camera frame. Defaults to '_link'.
- *~tf_timeout* (float): Number of seconds to wait for a transform between the map and camera frame before timeing out.

---

### goal_server.py

Sends 3D points in the map frame to the movebase Action server. Goals always have an orientation of [0, 0, 0] degrees.

#### Info

Default node name: *goal_server*

Dependencies: *rospy, actionlib, move_base_msgs, geometry_msgs, tf*

ROS Rate: *none*

#### Topics

##### Subscribes

- *goal_coords* (geometry_msgs/PointStamped): The goals as 3D points in the map frame.

#### Parameters

- *~map_frame* (string): Name of map frame. Defaults to 'map'.

## Launch files

