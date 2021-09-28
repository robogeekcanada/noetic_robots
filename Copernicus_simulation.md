<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# Copernicus Simulation

## 1. Installing Dependencies
Botsync Copernicus is a rugged and easy to integrate ground vehicle designed to support your prototyping and research needs. Copernicus supports the Robot Operating System (ROS) out of the box and provides access to motion commands through a serial interface.
**Source**: http://wiki.ros.org/Robots/Copernicus

### VELODYNE SIMULATOR
```bash
$ cd
$ mkdir -p velodyne_simulator/src
$ cd velodyne_simulator/src
$ git clone https://osilva77@bitbucket.org/DataspeedInc/velodyne_simulator.git
$ cd ..
$ catkin_make
$ echo 'source ~/velodyne_simulator/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### POINTCLOUD TO LASERSCAN
```bash
$ sudo apt-get update --fix-missing
$ sudo apt install ros-noetic-pointcloud-to-laserscan
```

### COPERNICUS SIMULATION
```bash
$ cd
$ mkdir -p copernicus_simulation/src
$ cd copernicus_simulation/src
$ git clone https://github.com/botsync/copernicus_simulation
$ cd ..
$ catkin_make
$ echo 'source ~/copernicus_simulation/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### COPERNICUS PHYSICAL ROBOT
```bash
$ cd
$ mkdir -p copernicus/src
$ cd copernicus/src
$ git clone https://github.com/botsync/copernicus.git
$ cd ..
$ catkin_make
$ echo 'source ~/copernicus/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
## 2. TESTING
If working with WSL, suggest to close all terminals and start them again before testing. To do a quick check packages have been installed `rospack list`

T1:
```bash
$ roslaunch copernicus_simulation gazebo.launch
```
T2:
```bash
$ roslaunch copernicus_simulation simulation.launch
```

### Troubleshooting:
Error due to xacro.py. We will need to modify `simulation.launch`  as shown below and rename file to`simulation2.launch` :

```bash
 <param name="robot_description" command="$(find xacro)/xacro $(arg model) imu_enabled:=$(arg wit_wt901c_imu) sick_lms151_enabled:=$(arg sick_lms151) velodyne_enabled:=$(arg velodyne_vlp16)"/>
```

Try again with the modified launch file:
```bash
$ roslaunch copernicus_simulation simulation2.launch
```

![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/Copernicus%20Simulation.PNG)

Success!! Happy to get this working. Haven't tested all functionality but I'll leave that as an exercise.

Check the official ROS page: http://wiki.ros.org/Robots/Copernicus to learn how to use Copernicus.
