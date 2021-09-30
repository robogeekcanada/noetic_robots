<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# ROBOTIS THORMANG MPC

[THOR](https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-MPC) -Tactical Hazardous Operations Robot - is an affordable, full size humanoid robot platform with advanced computational power, sophisticated sensors, high payload capacity, and dynamic motion abilities to enable many exciting researches and educational activities.

Source: http://wiki.ros.org/thormang3_mpc

## 1. Install Dependent Packages

### ROBOTIS MATH
```bash
$ cd
$ mkdir -p robotis_math/src
$ cd robotis_math/src 
$ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Math.git
$ cd ..
$ catkin_make
$ echo 'source ~/robotis_math/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### DYNAMIXEL SDK
``` bash
$ cd
$ mkdir -p dynamixel_sdk/src
$ cd dynamixel_sdk/src 
$ git clone https://github.com/ROBOTIS-GIT/DynamixelSDK.git
$ cd ..
$ catkin_make
$ echo 'source ~/dynamixel_sdk/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### DYNAMIXEL WORKBENCH MSGS
```bash
$ cd
$ mkdir -p dynamixel_workbench_msgs/src
$ cd dynamixel_workbench_msgs/src 
$ git clone https://github.com/ROBOTIS-GIT/dynamixel-workbench-msgs.git
$ cd ..
$ catkin_make
$ echo 'source ~/dynamixel_workbench_msgs/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### DYNAMIXEL WORKBENCH
```bash
$ cd
$ mkdir -p dynamixel_workbench/src
$ cd dynamixel_workbench/src 
$ git clone https://github.com/ROBOTIS-GIT/dynamixel-workbench.git
$ cd ..
$ catkin_make
$ echo 'source ~/dynamixel_workbench/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### ROBOTIS FRAMEWORK MSGS
```bash
$ cd
$ mkdir -p robotis_framework_msgs/src
$ cd robotis_framework_msgs/src 
$ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Framework-msgs.git
$ cd ..
$ catkin_make
$ echo 'source ~/robotis_framework_msgs/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### ROBOTIS FRAMEWORK COMMON
```bash
$ cd
$ mkdir -p robotis_framework/src
$ cd robotis_framework/src 
$ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-Framework.git
$ cd ..
$ catkin_make
$ echo 'source ~/robotis_framework/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### THORMANG3 ACTION MODULE MSGS
```bash
$ cd
$ mkdir -p thormang3_msgs/src
$ cd thormang3_msgs/src
$ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-msgs.git
$ cd ..
$ catkin_make
$ echo 'source ~/thormang3_msgs/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### ROBOTIS THORMANG COMMON
```bash
$ cd
$ mkdir -p thormang_common/src
$ cd thormang_common/src 
$ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-Common.git
$ cd ..
$ catkin_make
$ echo 'source ~/thormang_common/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### ROBOTIS WORKSPACE
```bash
$ cd
$ mkdir -p robotis_ws/src
$ cd robotis_ws/src 
$ git clone https://github.com/ROBOTIS-GIT/ROBOTIS-THORMANG-MPC.git
$ cd ..
$ catkin_make
$ echo 'source ~/robotis_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

## 2. Simulation

```bash
$ roslaunch thormang3_gazebo robotis_world2.launch
```

Fixed `robotis_world.launch` file by removing `.py` from `xacro.py` and renamed it to `robotis_world2.launch`

![Thormang3_Simulation](https://github.com/robogeekcanada/noetic_robots/blob/main/Thormang3_Simulation.PNG)

Works like a charm. Haven't tested the rest of functionality but suggest you go over this tutorial to test:  https://emanual.robotis.com/docs/en/platform/thormang3/gazebo_simulation/#gazebo-simulation



Happy Coding!
