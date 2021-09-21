# TIAGo Tutorials

Based on this repo: https://github.com/pal-robotics/tiago_tutorials last updated ROS Kinetic with Python 2.
There are OpenCV compatibility issues in C++. Haven't tested all tutorials, so there maybe more errors. 
Please share any issues and will update the tutorial accordingly. 

## Pre-requisite: 
Complete https://github.com/robogeekcanada/noetic_robots/blob/main/tiago_simulation_noetic.md

## 1. BUILD DEPENDENT PACKAGES

Let's start fixing dependent packages...

### ARUCO ROS
```
$ cd
$ mkdir -p aruco_ros/src
$ cd aruco_ros/src
$ git clone https://github.com/pal-robotics/aruco_ros.git
$ cd ..
$ catkin_make
$ echo 'source ~/aruco_ros/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### PAL WATSON
```
$ cd
$ mkdir -p pal_watson/src
$ cd pal_watson/src
$ git clone https://github.com/pal-robotics/pal_watson.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_watson/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### HUMANOID MSGS
```
$ cd
$ mkdir -p humanoid_msgs/src
$ cd humanoid_msgs/src
$ git clone https://github.com/ahornung/humanoid_msgs.git
$ cd ..
$ catkin_make
$ echo 'source ~/humanoid_msgs/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### PAL MSGS
```
$ cd
$ mkdir -p pal_msgs/src
$ cd pal_msgs/src
$ git clone https://github.com/pal-robotics/pal_msgs.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_msgs/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### TIAGO TUTORIALS
```
$ cd
$ mkdir -p tiago_tutorials/src
$ cd tiago_tutorials/src
$ git clone https://github.com/pal-robotics/tiago_tutorials.git
$ cd ..
$ catkin_make
$ echo 'source ~/tiago_tutorials/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

Most likely you will encounter many errors when building this package, I will list the ones I encountered and what I did to fix them.

#### Fix error with building Tiago Tutorials `segment.cfg` file

Remove 0 (Zero) on the left, change value to just zero 010 -> 0
File location: tiago_tutorials/src/tiago_tutorials/tiago_pcl_tutorial/cfg/

#### Fix OpenCV errors -old version not compatible

Replace CV_ with cv::

For example:
Change `CV_WINDOW_FREERATIO` to `cv::WINDOW_FREERATIO`
Change `CV_RANSAC` to `cv::RANSAC`

It affects more than one file, so be patient. 
Compile again until you are free of errors, and **don't forget to source tiago_tutorials**.

## 2. Testing Demo Motions

Once you are able to succesful compiled tiago_tutorials workspace, then:

```
$ roslaunch tiago_gazebo tiago_gazebo2.launch
$ roslaunch demo_motions motions.launch
```
Hint: Follow the additional instructions to enable motion.



