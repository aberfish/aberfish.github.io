---
title: Status
---

\[last updated *21 July 2022*]

### Complete
 - Basic obstacle avoidance using RTABMap, DWAplanner and movebase
 - Tracking Tango using the overhead camera
 - Sending overhead camera pixel coordinates as goal positions to Tango

### In progress
 - Commanding Tango to follow a list of coordinates from a csv file
 
### To do
 - Improve path following to smooth movements out
 - Improve overhead camera tracking to remove noise and increase accuracy
 - Setup tango_controller repo as a ROS package
 - Have tango_controller listen to movebase action server for goal status to decide when to send next goal coordinate