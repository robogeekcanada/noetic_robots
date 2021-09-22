<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# PR2 Simulator installation for ROS Noetic

PR2 has a special place in the ROS community heart http://wiki.ros.org/Robots/PR2. 
PR2 is written entirely in ROS, it was open sourced and so many roboticist learned experimenting with this cool robot.

The goal of this tutorial is to make PR2 Simulation package work in ROS Noetic. The last build was ROS Kinetic with Python 2, so a bit of work to do.

## 1. Install Dependencies for SDformat:
Reference: http://sdformat.org/tutorials?tut=install
```
$ sudo apt-get install ruby-dev build-essential libtinyxml-dev libboost-all-dev cmake mercurial pkg-config
$ sudo apt-get install libignition-math4-dev
```
## 2. Building SDformat:
Reference: http://sdformat.org/

**MAKE SURE TO BE IN THE HOME DIRECTORY**
```
$ cd
$ mkdir ~/sdf_source
$ cd ~/sdf_source/
$ git clone https://github.com/osrf/sdformat
$ cd sdformat
$ git checkout sdf6
$ mkdir build
$ cd build
$ cmake .. -DCMAKE_INSTALL_PREFIX=/usr
$ make -j4
$ make install
```
If you encounter error, try `$ sudo make install`

## 3. Install ROS Convex Decomposition
Reference: http://wiki.ros.org/convex_decomposition

**MAKE SURE TO BE IN THE HOME DIRECTORY**
```
$ cd
$ mkdir convex_ws
$ cd convex_ws/
$ mkdir src
$ cd src/
$ git clone https://github.com/ros/convex_decomposition.git
$ cd ..
$ catkin_make
$ echo 'source ~/convex_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

## 4. Install ROS ivcon
Reference: http://wiki.ros.org/ivcon

**MAKE SURE TO BE IN THE HOME DIRECTORY**
```
$ cd
$ mkdir ivcon_ws
$ cd ivcon_ws/
$ mkdir src
$ cd src/
$ git clone https://github.com/ros/ivcon.git
$ cd ..
$ catkin_make
$ echo 'source ~/ivcon_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

## 5. Create workspace for PR2:

**MAKE SURE TO BE IN THE HOME DIRECTORY**
```
$ cd
$ mkdir pr2_ws
$ cd pr2_ws/
$ mkdir src
$ cd src/
$ git clone -b noetic-devel https://github.com/PR2/pr2_simulator.git
$ git clone https://github.com/PR2/pr2_mechanism.git
$ git clone https://github.com/PR2/pr2_common.git
$ git clone https://github.com/PR2/pr2_mechanism_msgs.git
$ cd ..
$ catkin_make
```

## 6. Troubleshooting Compiling errors

If error with sdformat, we will need to make changes to `CMakeLists.txt` file in `pr2_gazebo_plugins/`

Reference: https://github.com/PR2/pr2_simulator/pull/149/files/70f23b87056c0259686063d686497c6be1fba476#diff-f60537da2561b1f991e2535dc660c629dbb876df72e7930a289252b2bb030c75

Go to: `pr2_gazebo_plugins/CMakeLists.txt`

```
$ cd  ~/pr2_ws/src/pr2_simulator/pr2_gazebo_plugins
$ gedit CMakeLists.txt
```

![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/pr2_troubleshooting.jpg)

**Remove red lines, add the green lines**

Finally save and exit file. Compile again, 
```
$ cd ~/pr2_ws/
$ catkin_make
```
If compiling fails due to C++ version, modify `CMakeLists.txt` in `~/pr2_ws/src/` 
	
```
$ sudo gedit CMakeLists.txt
```  
Add to CMakeLists.txt file as shown in picture below

```
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
```
![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/pr2_cplus_error.png)

Finally save and exit file. Compile again, 
```
$ cd ~/pr2_ws/
$ catkin_make
```

When compiling is successful, then complete installation by:
```
$ echo 'source ~/pr2_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

# Testing PR2 Simulator is working:

Reference: http://wiki.ros.org/pr2_simulator/Tutorials/StartingPR2Simulation

```
T1: 
$ roscore
T2
$ roslaunch gazebo_ros empty_world.launch
T3
$ roslaunch pr2_gazebo pr2.launch
```
![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/pr2_simulation.jpg)






