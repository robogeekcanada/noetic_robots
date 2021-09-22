<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# TIAGo Simulation installation in ROS NOETIC

In this tutorial we will build TIAGo Simulation from source to be able to run in ROS Kinetic. We will fix all dependencies in the process as well.
Last build of TIAGo was ROS Kinetic with Python 2.

Please start by reviewing how TIAGo works by visiting: http://wiki.ros.org/Robots/TIAGo 

## Assumptions:
1. You are not new to ROS, have a bit of experience with building packages and know how to launch nodes.
2. This tutorial has been tested in Ubuntu 20.04 and WSL Ubuntu 20.04
3. Some basic knowledge of OpenCV, C++ and Python.
4. You have a few hours to work on this. It's a bit tedious. I personally enjoy the process of fixing the issues one at the time.

## 1. Create TIAGo Workspace: tiago_ws

```
$ cd
$ mkdir -p tiago_ws/src
$ cd tiago_ws/src/
$ git clone https://github.com/pal-robotics/tiago_simulation.git
$ cd ..
$ catkin_make
$ echo 'source ~/tiago_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

## 2. Build the Dependent packages

### PAL Gazebo Worlds
```
$ cd
$ mkdir -p pal_gw_ws/src
$ cd pal_gw_ws/src
$ git clone https://github.com/pal-robotics/pal_gazebo_worlds.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_gw_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### TIAGO ROBOT
```
$ cd
$ mkdir -p tiago_robot_ws/src
$ cd tiago_robot_ws/src
$ git clone https://github.com/pal-robotics/tiago_robot.git
$ cd ..
$ catkin_make
$ echo 'source ~/tiago_robot_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### TIAGO DESCRIPTION CALIBRATION
```
$ cd
$ mkdir -p tiago_desc_calib_ws/src
$ cd tiago_desc_calib_ws/src
$ git clone https://github.com/pal-robotics/tiago_description_calibration.git
$ cd ..
$ catkin_make
$ echo 'source ~/tiago_desc_calib_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### PMB2 ROBOT
```
$ cd
$ mkdir -p pmb2_robot/src
$ cd pmb2_robot/src/
$ git clone https://github.com/pal-robotics/pmb2_robot.git
$ cd ..
$ catkin_make
$ echo 'source ~/pmb2_robot/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### HEY5 DESCRIPTION
```
$ cd
$ mkdir -p hey5_ws/src
$ cd hey5_ws/src/
$ git clone https://github.com/pal-robotics/hey5_description.git
$ cd ..
$ catkin_make
$ echo 'source ~/hey5_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### PAL GRIPPER DESCRIPTION
```
$ cd
$ mkdir -p pal_gripper_ws/src
$ cd pal_gripper_ws/src
$ git clone https://github.com/pal-robotics/pal_gripper.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_gripper_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### FOUR WHEEL STEERING MSGS
```
$ cd
$ mkdir -p fourwheel_ws/src
$ cd fourwheel_ws/src
$ git clone https://github.com/ros-drivers/four_wheel_steering_msgs.git
$ cd ..
$ catkin_make
$ echo 'source ~/fourwheel_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### URDF GEOMETRY PARSER
```
$ cd
$ mkdir -p urdf_parser_ws/src
$ cd urdf_parser_ws
$ git clone https://github.com/ros-controls/urdf_geometry_parser.git
$ cd ..
$ catkin_make
$ echo 'source ~/urdf_parser_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### IMU SENSOR CONTROLLER
```
$ cd
$ mkdir -p imu_sensor_ws/src
$ cd imu_sensor_ws/src
$ git clone https://github.com/ros-controls/ros_controllers.git
$ cd ..
$ catkin_make
$ echo 'source ~/imu_sensor_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### TIAGO MOVEIT CONFIG
```
$  cd
$ mkdir -p tiago_moveit/src
$ cd tiago_moveit/src
$ git clone https://github.com/pal-robotics/tiago_moveit_config.git
$ cd ..
$ catkin_make
$ echo 'source ~/tiago_moveit/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### HEAD ACTION
```
$ cd
$ mkdir -p pal_head_ws/src
$ cd pal_head_ws/src
$ git clone https://github.com/pal-robotics/head_action.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_head_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### SIMPLE GRASPING ACTION
```
$ cd
$ mkdir -p pal_simple_grasp/src
$ cd pal_simple_grasp/src
$ git clone https://github.com/pal-robotics/simple_grasping_action.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_simple_grasp/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### MOVEIT ROS PLANNING
```
$ sudo apt-get install ros-noetic-moveit-ros-planning-interface
```

### PLAY ACTION
```
$ cd
$ mkdir -p play_motion_ws/src
$ cd play_motion_ws/src
$ git clone https://github.com/pal-robotics/play_motion.git
$ cd ..
$ catkin_make
$ echo 'source ~/play_motion_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### TF LOOKUP
```
$ cd
$ mkdir -p tf_lookup_ws/src
$ cd tf_lookup_ws/src
$ git clone https://github.com/pal-robotics/tf_lookup.git
$ cd ..
$ catkin_make
$ echo 'source ~/tf_lookup_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### ROBOT STATE PUBLISHER
```
$ cd
$ mkdir -p pal_robot_state_publisher/src
$ cd pal_robot_state_publisher/src
$ git clone https://github.com/pal-robotics/robot_state_publisher.git
$ catkin_make
$ echo 'source ~/pal_robot_state_publisher/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### PMB2 ROBOT
```
$ cd
$ mkdir -p pmb2_robot_ws/src
$ cd pmb2_robot_ws/src
$ git clone https://github.com/pal-robotics/pmb2_robot.git
$ cd ..
$ catkin_make
$ echo 'source ~/pmb2_robot_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### TIAGO DUAL ROBOT
```
$ cd
$ mkdir -p tiago_dual_robot_ws/src
$ cd tiago_dual_robot_ws/src
$ git clone https://github.com/pal-robotics/tiago_dual_robot.git
$ cd ..
$ catkin_make
$ echo 'source ~/tiago_dual_robot_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

## 3. FIX OTHER ISSUES

### Make joystick_relay.py executable:
```
$ cd /opt/ros/noetic/lib/twist_mux
$ sudo chmod +x joystick_relay.py
```
### Fix Python compatibility Python 2 to Python 3
This may not be required if you can command `python` with no errors
```
$ sudo apt install python-is-python3
```
### FIX YAML files
YAML files were missing when sourcing from https://github.com/pal-robotics/tiago_simulation.git.
The melodic-devel branch has them, so I just copied them and place them. If you want to clone from melodic-devel, it should be fine too, but I was already few hours into troubleshooting.

Copied missing YAML from the melodic version:

https://github.com/ros-controls/ros_controllers/blob/melodic-devel/imu_sensor_controller/imu_sensor_controller.yaml
https://github.com/ros-controls/ros_controllers/blob/melodic-devel/force_torque_sensor_controller/force_torque_sensor_controller.yaml

### FIX LAUNCH FILE
Error: Can't start throttle_filtering_points launch:
 
Removed reference to this node from launch, modify and save it as tiago_gazebo2.launch modified. 
I spent a lot of time trying to fix this but unsuccessful.

File location: tiago_ws/src/tiago_simulation/tiago_gazebo/launch
```
  <!-- point cloud throttle and filter -->
  <group unless="$(arg public_sim)">
    <include file="$(find pal_pcl_points_throttle_and_filter)/launch/throttle_filtering_points.launch">
      <arg name="cloud"  value="/xtion/depth_registered/points"/>
    </include>
  </group>
```

## 4. TEST LAUNCH FILE
That's it, ready to test.

```
$ cd tiago_ws/src/tiago_simulation/tiago_gazebo/launch/
$ roslaunch tiago_gazebo tiago_gazebo2.launch
```

![Image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/TIAGo_simulation.jpg)


You made it! Well done. Next step make TIAGo Tutorials work.





