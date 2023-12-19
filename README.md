# RPLidar Hector SLAM
Using Hector SLAM without odometry data on a ROS system with the RPLidar A1.

1. Install ROS full desktop version (tested on Kinetic) from: http://wiki.ros.org/kinetic/Installation/Ubuntu
2. Create a catkin workspace: http://wiki.ros.org/ROS/Tutorials/CreatingPackage
3. Create catkin workspace (working link): https://www.instructables.com/Getting-Started-With-the-Low-cost-RPLIDAR-Using-Je/
4. Clone this repository into your catkin workspace
5. In your catkin workspace run `source /devel/setup.bash`
6. Run `chmod 666 /dev/ttyUSB0` or the serial path to your lidar
7. Run `roslaunch rplidar_ros rplidar.launch`
8. Run `roslaunch hector_slam_launch tutorial.launch`
9. RVIZ should open up with SLAM data

# Working links
https://collabnix.com/getting-started-with-the-low-cost-rplidar-using-jetson/

## Issues

[Fix] rosdep: command not found issue
https://github.com/jugfk/installROS/issues/2

CMAKE_PREFIX_PATH doesn't help CMake in finding Qt5
https://stackoverflow.com/questions/47647035/cmake-prefix-path-doesnt-help-cmake-in-finding-qt5

Project 'cv_bridge' can not find opencv
https://github.com/ros-perception/vision_opencv/issues/345#issuecomment-663416626

# Sources
[RPLidar](https://github.com/robopeak/rplidar_ros)<br />
[Hector_SLAM](https://github.com/tu-darmstadt-ros-pkg/hector_slam)<br />
[Fixing launch files](https://hackaday.io/project/7284-oscar-omni-service-cooperative-assistant-robot/log/26164-first-foray-into-ros) (only needed if you are using the original hector slam repository)
- In `catkin_ws/src/rplidar_hector_slam/hector_slam/hector_mapping/launch/mapping_default.launch` <br />
__replace the second last line with__ <br />
`<node pkg="tf" type="static_transform_publisher" name="base_to_laser_broadcaster" args="0 0 0 0 0 0 base_link laser 100" />`<br />
__the third line with__<br />
`<arg name="base_frame" default="base_link"/>`<br />
__the fourth line with__<br />
`<arg name="odom_frame" default="base_link"/>`
- In `catkin_ws/src/rplidar_hector_slam/hector_slam/hector_slam_launch/launch/tutorial.launch` <br />
__replace the third line with__<br />
`<param name="/use_sim_time" value="false"/>`
