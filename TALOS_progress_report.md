# TALOS Simulator in ROS Noetic

[TALOS](http://wiki.ros.org/Robots/TALOS) is a commercial humanoid robot of PAL Robotics. The last build of the TALOS Simulator were done for ROS Melodic: https://github.com/pal-robotics/talos_tutorials in May 2020.

## 1. Install Dependencies

The `rosinstall` file is available, we will use `talos_public-melodic.rosinstall` as a reference.

```bash
- git: {local-name: gazebo_ros_pkgs, uri: 'cl', version: 'melodic-devel'}
- git: {local-name: pal_gazebo_plugins, uri: 'https://github.com/pal-robotics/pal_gazebo_plugins.git', version: 'melodic-devel'}
- git: {local-name: pal_gazebo_worlds, uri: 'https://github.com/pal-robotics/pal_gazebo_worlds.git', version: 'kinetic-devel'}
- git: {local-name: pal_hardware_gazebo, uri: 'https://github.com/pal-robotics/pal_hardware_gazebo.git', version: 'melodic-devel'}
- git: {local-name: pal_hardware_interfaces, uri: 'https://github.com/pal-robotics/pal_hardware_interfaces.git', version: 'indigo-devel'}
- git: {local-name: pal_msgs, uri: 'https://github.com/pal-robotics/pal_msgs.git', version: 'indigo-devel'}
- git: {local-name: pal_transmissions, uri: 'https://github.com/pal-robotics/pal_transmissions', version: 'kinetic-devel'}
- git: {local-name: play_motion, uri: 'https://github.com/pal-robotics/play_motion.git', version: 'kinetic-devel'}
- git: {local-name: roboticsgroup_gazebo_plugins, uri: 'https://github.com/pal-robotics-forks/roboticsgroup_gazebo_plugins.git', version: 'kinetic-devel'}
- git: {local-name: ros_control, uri: 'https://github.com/pal-robotics-forks/ros_control.git', version: 'kinetic-devel'}
- git: {local-name: ros_controllers, uri: 'https://github.com/pal-robotics-forks/ros_controllers.git', version: 'kinetic-devel'}
- git: {local-name: talos_moveit_config, uri: 'https://github.com/pal-robotics/talos_moveit_config.git', version: 'indigo-devel'}
- git: {local-name: talos_robot, uri: 'https://github.com/pal-robotics/talos_robot.git', version: 'kinetic-devel'}
- git: {local-name: talos_simulation, uri: 'https://github.com/pal-robotics/talos_simulation.git', version: 'kinetic-devel'}
- git: {local-name: tf_lookup, uri: 'https://github.com/pal-robotics/tf_lookup.git', version: 'master'}
- git: {local-name: head_action, uri: 'https://github.com/pal-robotics/head_action.git', version: 'indigo-devel'}
- git: {local-name: dynamic_introspection, uri: 'https://github.com/pal-robotics/dynamic_introspection', version: 'kinetic-devel'}
- git: {local-name: backward_ros, uri: 'https://github.com/pal-robotics/backward_ros', version: 'kinetic-devel'}
- git: {local-name: pal_statistics, uri: 'https://github.com/pal-robotics/pal_statistics', version: 'kinetic-devel'}
- git: {local-name: humanoid_msgs, uri: 'https://github.com/ahornung/humanoid_msgs.git', version: 'master'}
```

## 2. Building Dependent Packages

Based on the experience with the TIAGO simulator, refer to this [tutorial](https://github.com/robogeekcanada/noetic_robots/blob/main/tiago_tutorials.md). It's unlikely that it will work without a bit of work, especially due to incompatibility with OpenCV. So we will source each package individually. We will also avoid installing `gazebo_ros_packages` to prevent conflicts. The **sequence** **of installation** is very important as some packages are dependent of others.

### DDynamic_reconfigure
Not listed but needed for `pal_gazebo_plugins`
```bash
$ cd
$ mkdir -p ddynamic_reconfigure/src
$ cd ddynamic_reconfigure/src
$ git clone https://github.com/pal-robotics/ddynamic_reconfigure.git
$ cd ..
$ catkin_make
$ echo 'source ~/ddynamic_reconfigure/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### PAL GAZEBO PLUGINS
```bash
$ cd
$ mkdir -p pal_gazebo_plugins/src
$ cd pal_gazebo_plugins/src
$ git clone https://github.com/pal-robotics/pal_gazebo_plugins.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_gazebo_plugins/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### PAL GAZEBO WORLDS
```bash
$ cd
$ mkdir -p pal_gazebo_worlds/src
$ cd pal_gazebo_worlds/src
$ git clone https://github.com/pal-robotics/pal_gazebo_worlds.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_gazebo_worlds/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### PAL HARDWARE INTERFACES
```bash
$ cd
$ mkdir -p pal_hardware_interfaces/src
$ cd pal_hardware_interfaces/src
$ git clone https://github.com/pal-robotics/pal_hardware_interfaces.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_hardware_interfaces/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### PAL STATISTICS
```bash
$ cd
$ mkdir -p pal_statistics/src
$ cd pal_statistics/src
$ git clone https://github.com/pal-robotics/pal_statistics
$ cd ..
$ catkin_make
$ echo 'source ~/pal_statistics/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### BACKWARD ROS
```bash
$ cd
$ mkdir -p backward_ros/src
$ cd backward_ros/src
$ git clone https://github.com/pal-robotics/backward_ros
$ cd ..
$ catkin_make
$ echo 'source ~/backward_ros/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### DYNAMIC INTROSPECTION
```bash
$ cd
$ mkdir -p dynamic_introspection/src
$ cd dynamic_introspection/src
$ git clone https://github.com/pal-robotics/dynamic_introspection
$ cd ..
$ catkin_make
$ echo 'source ~/dynamic_introspection/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
### GAZEBO ROS PKGS
```bash
$ cd
$ mkdir -p gazebo_ros_pkgs/src
$ cd gazebo_ros_pkgs/src
$ git clone -b noetic-devel https://github.com/pal-robotics-forks/gazebo_ros_pkgs.git
$ cd ..
$ catkin_make
$ echo 'source ~/gazebo_ros_pkgs/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### PAL HARDWARE GAZEBO
```bash
$ cd
$ mkdir -p pal_hardware_gazebo/src
$ cd pal_hardware_gazebo/src
$ git clone https://github.com/pal-robotics/pal_hardware_gazebo.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_hardware_gazebo/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

**Sept 27-2021:**
With Gazebo ROS PKGS compiled, then PAL Hardware Gazebo compiled no issues as well

**Sept 25-2021: Compiling errors**:

1. For now commented line 280, will get back to it -- not good to mess with transmission :|
2. Second error is an open issue since Nov 2020 https://github.com/pal-robotics/pal_hardware_gazebo/issues/4. It requires the use `gazebo_ros_pkgs` but that means uninstalling and affecting other dependencies, so not a good solution. Comment lines for now, let's see what happens. It compiles but of course we need to fix this.

### PAL MSGS
```bash
$ cd
$ mkdir -p pal_msgs/src
$ cd pal_msgs/src
$ git clone https://github.com/pal-robotics/pal_msgs.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_msgs/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### PLAY MOTION
```bash
$ cd
$ mkdir -p play_motion/src
$ cd play_motion/src
$ git clone https://github.com/pal-robotics/play_motion.git
$ cd ..
$ catkin_make
$ echo 'source ~/play_motion/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### ROS CONTROL
```bash
$ cd
$ mkdir -p ros_control/src
$ cd ros_control/src
$ git clone https://github.com/pal-robotics/ros_control.git
$ cd ..
$ catkin_make
$ echo 'source ~/ros_control/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### ROS CONTROLLERS
```bash
$ cd
$ mkdir -p ros_controllers/src
$ cd ros_controllers/src
$ git clone https://github.com/pal-robotics/ros_controllers.git
$ cd ..
$ catkin_make
$ echo 'source ~/ros_controllers/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### TALOS MOVEIT CONFIG
```bash
$ cd
$ mkdir -p talos_moveit_config/src
$ cd talos_moveit_config/src
$ git clone https://github.com/pal-robotics/talos_moveit_config.git
$ cd ..
$ catkin_make
$ echo 'source ~/talos_moveit_config/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### TALOS SIMULATION
```bash
$ cd
$ mkdir -p talos_simulation/src
$ cd talos_simulation/src
$ git clone https://github.com/pal-robotics/talos_simulation.git
$ cd ..
$ catkin_make
$ echo 'source ~/talos_simulation/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### HEAD ACTION
```bash
$ cd
$ mkdir -p pal_head_ws/src
$ cd pal_head_ws/src
$ git clone https://github.com/pal-robotics/head_action.git
$ cd ..
$ catkin_make
$ echo 'source ~/pal_head_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### TF LOOKUP
```bash
$ cd
$ mkdir -p tf_lookup_ws/src
$ cd tf_lookup_ws/src
$ git clone https://github.com/pal-robotics/tf_lookup.git
$ cd ..
$ catkin_make
$ echo 'source ~/tf_lookup_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### HUMANOID MSGS
```bash
$ cd
$ mkdir -p humanoid_msgs/src
$ cd humanoid_msgs/src
$ git clone https://github.com/ahornung/humanoid_msgs.git
$ cd ..
$ catkin_make
$ echo 'source ~/humanoid_msgs/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### ROBOTICS GROUP GAZEBO PLUGINS
```bash
$ cd
$ mkdir -p robotics_group_gazebo_plugins/src
$ cd robotics_group_gazebo_plugins/src
$ git clone https://github.com/pal-robotics-forks/roboticsgroup_gazebo_plugins.git
$ cd ..
$ catkin_make
$ echo 'source ~/robotics_group_gazebo_plugins/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
### RBDL
```bash
$ git clone --recursive https://github.com/ORB-HD/rbdl-orb
$ mkdir rbdl-build
$ cd rbdl-build
$ cmake .. -DRBDL_BUILD_PYTHON_WRAPPER=ON -DCMAKE_INSTALL_PREFIX=~/catkin_ws/rbdl_ws/install -DRBDL_BUILD_ADDON_URDFREADER=ON -DRBDL_USE_ROS_URDF_LIBRARY=OFF -Wno-dev
$ make
$ make install
```
**Credit:** https://www.reddit.com/r/ROS/comments/phl7nk/install_rbdlorb_on_ros_noetic/

### TALOS ROBOT
```bash
$ cd
$ mkdir -p talos_robot2/src
$ cd talos_robot2/src
$ git clone -b dae_meshes_with_color https://github.com/pal-robotics/talos_robo
t.git
$ cd ..
$ catkin_make
$ echo 'source ~/talos_robot2/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc

```
**Compiling error**: Couldn't link, several attempts. Raised [ROS question](https://answers.ros.org/question/387398/how-to-add-so-file-to-catkin-workspace/ )

**Fix:** Decided to clone the latest branch instead `dae_meshes_with_color`.

### PAL TRANSMISSIONS
```bash
$ cd
$ mkdir -p pal_transmissions/src
$ cd pal_transmissions/src
$ git clone https://github.com/pal-robotics/pal_transmissions
$ cd ..
$ catkin_make
$ echo 'source ~/pal_transmissions/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```
Compiling Errors too many but will take a look at the latest branch of `talos_robot` for clues

# Progress Notes: Sept 27-2021

1. Good news only one pending dependency left to compile: PAL TRANSMISSIONS
2. ~~Concerns about Gazebo dependencies~~ All Gazebo dependencies built.
3. ~~Hardware compiling errors may require more time than I expected. 
One approach may be to compile old libraries but based on the readings it may cause issues on behaviours, so I will go on the route of fixing by using the current ROS Control libraries but not sure what I am getting myself into.~~ Found ways to fix as per progress report
4. ~~RBDL installation is not trivial, so I will study before proceeding on installing this library, but it will my next action to take.~~ RBDL installed
5. Tested some of the launch files, they worked, however Gazebo launch files don't work due to xml incompatiblities. Will work on that next.

I will keep the updates. If you have any ideas please share.
