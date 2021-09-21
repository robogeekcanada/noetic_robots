# STDR Simulator

Tutorial to run STDR Simulator in ROS Noetic. HAven't been mantained for a while. Last build ROS Indigo.

## 1. Create Workspace

```
$ mkdir stdr_ws
$ cd stder_ws
$ mkdir src
$ cd src
$ git clone https://github.com/stdr-simulator-ros-pkg/stdr_simulator.git
$ cd ..
$ rosdep install --from-paths src --ignore-src --rosdistro $ROS_DISTRO
```

If failure libqt4 related:
```
$ sudo add-apt-repository ppa:rock-core/qt4
$ sudo apt update
$ sudo apt-get install libqt4-dev
```

Then try again and complete install...
$ rosdep install --from-paths src --ignore-src --rosdistro $ROS_DISTRO
$ catkin_make
$ gedit ~/.bashrc
$ Add at the end:
$ source ~/stdr_ws/devel/setup.bash

## 2. Testing

```
$ roslaunch stdr_launchers server_with_map_and_gui_plus_robot.launch
```

![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/STDR_simulation.jpg)

## 3. Pending work:
Test all the tutorials: Refer to the following tutorials:
http://wiki.ros.org/stdr_simulator/Tutorials
