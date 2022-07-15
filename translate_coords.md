[Home](index.md)
# translate_coords documentation 

## Package overview  
    
The translate_coords package currently converts 2d pixel coordinates from the camera frame to 3d coordinates in the real world frame. The camera is a realsense d435. *soon it will be able to convert 3d coordinates in the real world frame into coordinates for the rtab map coordinate frame.*  

## scripts
  
### cam_depthcoords.py  
  
This script converts the pixel coordinates from the camera frame to 3d coordinates in the real world frame. It initialises one node 'cam_to_depthcoords'. 
  
'cam_to_depthcoords' subscribes to:  
  
- '/camera/depth/camera_info', message type: CameraInfo  
This topic provides data about the intrinsic camera parameters.  
  
- '/camera/aligned_depth_to_color/image_raw', message type: Image  
This topic provides frame by frame image data from the camera  
  
- 'input_coords', message type: Point  
This topic provides the 2d coordinates that are to be converted from pixel to real world.

'cam_to_depth_coords' publishes to:  
  
- 'realworld_coords', message type: Point.
Once the conversion has occured the 3d real world point is published to this topic.

### cam_transform.py

### goal_server.py

## How to run 

