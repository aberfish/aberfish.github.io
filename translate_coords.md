[Home](index.md)
# translate_coords documentation 

## Package overview  
    
The translate_coords package currently converts 2d pixel coordinates from the camera frame to 3d coordinates in the real world frame. The camera is a realsense d435. *soon it will be able to convert 3d coordinates in the real world frame into coordinates for the rtab map coordinate frame.*  

## scripts
  
### cam_depthcoords.py  
  
This script converts the pixel coordinates from the camera coordinate system to 3d coordinates (in meters) in the real world camera coordinate system. 

It initialises one node 'cam_to_depthcoords'. 
  
'cam_to_depthcoords' subscribes to:  
  
- '/camera/depth/camera_info', message type: CameraInfo  
This topic provides data about the intrinsic camera parameters.  
  
- '/camera/aligned_depth_to_color/image_raw', message type: Image  
This topic provides frame by frame image data from the camera  
  
- 'input_coords', message type: Point  
This topic provides the 2d coordinates that are to be converted from pixel to real world.

'cam_to_depth_coords' publishes to:  
  
- 'depth_coords', message type: Point.
Once the conversion has occured the 3d real world point is published to this topic. 

### cam_transform.py

This script broadcasts a description of a static transform from the map frame to the camera frame.  
  
It broadcasts the transform to '/tf_static' .
  
It initialises one node 'cam_tf_broadcaster'.
  
### depth_to_mapcoords.py

This script performs a translation on the point provided in the depth_coords topic. The point is currently in the real world cooridnate system with the camera at the origin of the coordinate axis. A transform is applied such that the point is now relative to the 'map' frame. The map frame is also in the real world coordinate system but the origin of the axis is the point where Tango physically starts from (marked with tape).

It initialises one node 'depth_to_mapcoords'

'depth_to_mapcoords' subscribes to:

- 'depth_coords', message type: Point

'depth_coords' publishes to:

- 'world-coords', message type: PointStamped.

### goal_server.py

## How to run 

