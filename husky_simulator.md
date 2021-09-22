<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# Husky Simulator Installation ROS Noetic Tutorial

## 1. Install Dependencies
Reference: http://wiki.ros.org/LMS1xx
```
$ sudo apt-get install ros-noetic-lms1xx
```
Reference: https://bitbucket.org/DataspeedInc/velodyne_simulator/src/master/
```
$ sudo apt-get install ros-noetic-velodyne-description
```
Reference: http://wiki.ros.org/robot_localization
```
$ sudo apt-get install ros-noetic-robot-localization
```
Reference: http://wiki.ros.org/interactive_marker_twist_server
```
$ sudo apt-get install ros-noetic-interactive-marker-twist-server
```
Reference: http://wiki.ros.org/twist_mux
```
$ sudo apt-get install ros-noetic-twist-mux
```
Reference: http://wiki.ros.org/joy
```
$ sudo apt-get install ros-noetic-joy
```
Reference: http://wiki.ros.org/teleop_twist_joy
```
$ sudo apt-get install ros-noetic-teleop-twist-joy
```
Reference: http://wiki.ros.org/dwa_local_planner
```
$ sudo apt-get install ros-noetic-dwa-local-planner
```

## 2. Create Husky workspace
```
$ mkdir husky_ws
$ cd husky_ws
$ mkdir src
$ cd src
$ git clone https://github.com/gmsanchez/husky.git
$ cd ..
$ catkin_make
$ echo 'source ~/husky_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

## 3. Launching simulation
```
$ cd
$ export HUSKY_GAZEBO_DESCRIPTION=$(rospack find husky_gazebo)/urdf/description.gazebo.xacro
$ roslaunch husky_gazebo husky_empty_world.launch
```
![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/husky_simulator.jpg)

No major issues encoutered other than installing a bunch of dependencies. 
I added the references as I believe there is interesting material that will make you understand how Husky works.

Enjoy!
