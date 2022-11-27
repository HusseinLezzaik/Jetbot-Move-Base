# Jetbot Move Base
Movebase configs to get started with Jetbot and the ZED2 camera

## Getting Started
1. Install ROS Kinetic or Melodic (depending on your ubuntu distro), follow steps [here](http://wiki.ros.org/melodic/Installation/Source).
2. Download the [ZED ROS](https://github.com/stereolabs/zed-ros-wrapper) wrapper from Stereo Labs, and compile code:
``` 
$ catkin_make -DCMAKE_BUILD_TYPE=Release
```
To test ZED2 camera run:
```
$ roslaunch zed_wrapper zed2.launch
```
3. Tune ZED2 camera parameters, turn off unuseful features to save memory/compute consumption.
4. Run some unit tests to make sure you're reading the correct sensory information. For more read [here](https://www.stereolabs.com/docs/ros/).
5. Install [Rviz](http://wiki.ros.org/rviz), and run rviz to see the outputs of the camera:
```
$ rosrun rviz rviz
```
6. Clone jetbot ROS from [here](https://github.com/dusty-nv/jetbot_ros), and compile code
7. Publish some numbers to `cmd_vel` and validate results in real life:
```
$ rostopic pub /cmd_vel geometry_msgs/Twist -r 3 -- '[0.5,0.0,0.0]' '[0.0, 0.0, 0.0]'
```
8. Clone the ROS navigation package from [here](https://github.com/ros-planning/navigation), and build the package.
9. Use params given in thsi repo to get started, but please note that due to some manufacturing reasons etc that you will probably need to do some tuning to get it to work for you.
10. Start by publishing simple commands like telling the robot to move forward by 1m for examle using command below:
```
$ rostopic pub /move_base_simple/goal geometry_msgs/PoseStamped '{header: {stamp: now, frame_id: "map"}, pose: {position: {x: 1.0, y: 0.0, z: 0.0}, orientation: {w: 1.0}}}'
```
11. Once validated, start working with more complex tasks.

## Frames
It's critical while building your ROS packages to make sure that all frames are interconnected and in order, use these commands to print the current graph of your current frames:
```
$ rosrun tf view_frames
$ evince frames.pdf
```

## Topics
To visualize the graph of how topics are all connected together, run the following command:
```
$ rosrun rqt_graph rqt_graph
```

## Notes
1. Robots in the real world are very sensitive to numbers, keep iterating and trying things until system works stabily. It's about finding the right combination of numbers, and ratio's between different frequencies. Sometimes a 2.5Hz frequency instead of 2.3Hz could make or break your work!
2. If you get stuck while running `catkin_make`, try using this magical command:
```
$ rosdep install --from-paths src --ignore-src -r -y
```
3. Use rviz to debug your bugs, if possible even add your monitor on top of your robot. It's much easier debugging problems like that instead of from the terminal.

Feel free to reach out to me for any questions! Always open for collaborations as well!
