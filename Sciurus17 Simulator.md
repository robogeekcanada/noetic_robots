<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# Sciurus17 Simulator

[Sciurus17](http://wiki.ros.org/sciurus17) is an upper-body humanoid robot equipped with 17 axes for the whole body and 19 axes for both hands. With a depth camera on the head and an RGB camera on the chest as standard equipment, you can immediately start advanced manipulation tasks that utilize image recognition.

## 1. SCIURUS17 ROS REPO
[Sciurus17 repo](https://github.com/rt-net/sciurus17_ros) is written in Japanese. If you are using Google Chrome, right click and select Translate to English. It looks like the last build was for ROS Kinetic but the repo is actively maintained. And per recommended environment it looks that there is also a working Melodic version which is good news as Noetic upgrades are easy from Melodic. Time will tell.

### Recommended environment:
- ROS Kinetic
  - OS: Ubuntu 16.04.5 LTS
  - ROS Distribution: Kinetic Kame 1.12.14
  - Rev 1.12.17
  - MoveIt! 0.9.17
  - Gazebo 7.0.0
- ROS Melodic
  - OS: Ubuntu 18.04.3 LTS
  - ROS Distribution: Melodic Morenia 1.14.3
  - Rev 1.12.16
  - MoveIt! 1.13.3
  - Gazebo 9.0.0

## 2. Building from Source

### Pre-requisites:
* Install [Intel RealSense SDK 2.0](https://github.com/IntelRealSense/librealsense) 
* Download and build the ROS package [realsense2_camera](http://wiki.ros.org/realsense2_camera) 

#### Ubuntu 20.04 Installation of Intel RealSense SDK 2.0
```bash
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
$ sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main" -u

$ sudo apt-get install librealsense2-dkms
$ sudo apt-get install librealsense2-utils

# Optional
$ sudo apt-get install librealsense2-dev
$ sudo apt-get install librealsense2-dbg

#Testing step if you have the camera but no needed for simulation
$ modinfo uvcvideo | grep "version:"
```

#### Build ROS Package `realsense2_camera`
```bash
$ sudo apt-get install ros-noetic-realsense2-camera
```

### Creating SCIURUS17 WORKSPACE
```bash
$ cd
$ mkdir -p sciurus_ws/src
$ cd sciurus_ws/src
$ git clone https://github.com/rt-net/sciurus17_ros.git
# package required for sciurus17_gazebo
$ git clone https://github.com/roboticsgroup/roboticsgroup_gazebo_plugins.git
$ rosdep install -r -y --from-paths . --ignore-src
$ cd ~/sciurus_ws && catkin_make
$ echo 'source ~/sciurus_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

## 3. Testing Simulation
```bash
$ roslaunch sciurus17_gazebo sciurus17_with_table2.launch
```

Lots of issues regarding loading urdf files. So in troubleshooting, decided to create a single urdf and test it in PyBullet first.
`sciurus17_with_table2.launch` to launch `sciurus17_3.urdf.xacro`

Still work in progress and will share when files completed. Basically I removed macros to simplify the troubleshooting.
Encouraging results URDF loads in PyBullet:

![Sciurus17_pybullet](https://github.com/robogeekcanada/noetic_robots/blob/main/images/Sciurus17_pybullet.PNG)

and Gazebo:

![Sciurus17_Gazebo](https://github.com/robogeekcanada/noetic_robots/blob/main/images/Sciurus17_Gazebo.PNG)

Motor control also working well as can be seen in the position of the arms and hands in this picture.

![Sciurus17_Camera](https://github.com/robogeekcanada/noetic_robots/blob/main/images/Sciurus17_Camera.PNG)

In the last revision of `sciurus17_3.urdf.xacro` transmission was also fixed. There are warnings regarding PID but that has to do with Gazebo control. 
The reader is welcome to pursue the final fix as a way to understand. Hint: Work on .yaml files fake controls.

# Final Conclusions
Working on Sciurus17 was a great experience. In the process I learned a lot how xacro:macro work and I spent more time on making the simulation to work but the code works
with minor changes as it was written in Python2.7. There is a folder of examples that I highly encourage the reader to go over them. 

Biggest challenge was to find information on this robot. The repo is in Japanese and thanks to Google Translate I was able to follow the instructions, however, the issues section, 
was not translated well so this time it was going back to the basics and understand how each component works.

