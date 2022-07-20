## Goals
Translate fish movements into a mobile robot control algorithm, allowing a mobile robot to learn from fish decision making and route selection.

Explore whether a robot can successfuly use fish as demonstrators within Learning by Demonstration models to complete a task.

## Status
\[last updated 20 July 2022]
### Complete
 - Basic obstacle avoidance using RTABMap, DWAplanner and movebase
 - Tracking Tango using the overhead camera
 - Sending overhead camera pixel coordinates as goal positions to Tango

### Inprogress
 - Commanding Tango to follow a list of coordinates from a csv file
 
### To-do
 - Improve path following to smooth movements out
 - Improve overhead camera tracking to remove noise and increase accuracy

## Pages
### FAQs and General Information
- [Working with Tango](tango.md)

### Package Documentation
- [PACKAGE - translate_coords](translate_coords.md)
- [PACKAGE - tango_tracker](tango-tracker.md)
- [PACKAGE - tango_rtabmap](tango_rtabmap)
