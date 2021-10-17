<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# Nao Simulator

Nao robot is 60cm tall humanoid targeted at research lab and classrooms. Nao is small, but it packs a lot into its tiny frame: four microphones, two VGA cameras, touch sensors on the head, infrared sensors, and more. 

The use of Nao with ROS has demonstrated how quickly open-source code can enable a community to come together around a common hardware platform. Most of the documents to make NAO Simulation work dates back to ROS Indigo, so not an easy task to make it work in ROS Noetic.

In this tutorial we will show how to spawn Nao model in Gazebo and control the joints with ROS control manager. 

With regards to `Naoqi interface`, currently it works with Python 2. I will share a link how to download it, however integration will require some more effort from the user end. 

## 1. Install Dependencies

### NAO VIRTUAL
```bash
$ cd
$ mkdir -p nao_virtual2/src
$ cd nao_virtual2/src
$ git clone https://github.com/ros-naoqi/nao_virtual.git
$ cd ..
$ catkin_make
$ echo 'source ~/nao_virtual2/devel/setup.bash' >> ~/.bashrc
$ source ~/.bashrc
```

### NAO ROBOT
```bash
$ cd
$ mkdir -p nao_robot/src
$ cd nao_robot/src
$ git clone https://github.com/ros-naoqi/nao_robot.git
$ cd ..
$ catkin_make
$ echo 'source ~/nao_robot/devel/setup.bash' >> ~/.bashrc
$ source ~/.bashrc
```

### NAO MESHES
```bash
$ cd
$ mkdir -p nao_meshes_ws/src
$ cd nao_meshes_ws/src
$ git clone https://github.com/ros-naoqi/nao_meshes.git
$ cd ..
$ catkin_make
$ echo 'source ~/nao_meshes_ws/devel/setup.bash' >> ~/.bashrc
$ source ~/.bashrc
```

### ROS CONTROLLERS
In case you don't have ROS Controllers, install the latest noetic version:
```bash
$ sudo apt-get install ros-noetic-ros-control ros-noetic-ros-controllers
```

## 2. MESHES INSTALLATION and License Agreement
First install Nao meshes following instructions below and accept the agreement conditions.

```bash
$ wget https://github.com/ros-naoqi/nao_meshes_installer/raw/master/naomeshes-0.6.7-linux-x64-installer.run
$ chmod +x naomeshes-0.6.7-linux-x64-installer.run
$ ./naomeshes-0.6.7-linux-x64-installer.run
```

<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/NAO%20meshes%20installer.PNG" alt="NAO meshes installer" style="zoom: 67%;" />

After installation, copy `meshes` and `texture` folders from `.ros` directory to `nao_meshes_ws/src/nao_meshes` directory

Make sure to enable **Show Hidden Files**

<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/hidden_files.jpg" alt="image-20211017145711591" style="zoom:50%;" />

**Source:**
<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/meshes_original_location.png" alt="meshes_original_location" style="zoom:50%;" />

**Destination:**
<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/meshes_destination.png" alt="meshes_destination" style="zoom:50%;" />


## 3. Fix URDF and Xacro files

A few changes are required. 

### Replace `nao.urdf`

This is in important step as many fixes were done to make it work. From this repo copy [nao.urdf](https://github.com/robogeekcanada/noetic_robots/blob/main/nao.urdf) file and replace the file with the same name located:

`nao_robot/src/nao_robot/nao_description/urdf/naoV40_generated_urdf/`

![replace_nao_urdf](https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/replace_nao_urdf.png)


### HARDWARE INTERFACE ISSUES

Add `hardware_interface/` in `naoTransmission.xacro` in every `<hardwareInterface>` tag as shown in the picture below:


```xml
<hardwareInterface>hardware_interface/PositionJointInterface</hardwareInterface>
```

<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/hardware_inteface.png" alt="hardware_inteface" style="zoom:50%;" />

### AnklePitch Joint Issue

There is a name collision in the original `nao.urdf` file that needs addressing. `AnklePitch`  **link** has the same name as `AnklePitch` **joint,**  so to fix we will change the joint name to  `AnklePitchJoint`  in the following files:  `nao.urdf` , `naoTranmission.xacro` and `nao_legs.xacro`.

<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/name_collision.jpg" alt="name_collision" style="zoom: 67%;" />

<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/nao_xacro_transmission.png" alt="nao_xacro_transmission" style="zoom:50%;" />

<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/nao_legs_xacro.png" alt="nao_legs_xacro" style="zoom:50%;" />

Also we have to fix config files in `nao_virtual2/src/nao_virtual/nao_control/config/` and `nao_gazebo_plugin/config` folders. 

<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/nao_config_files.png" alt="nao_config_files" style="zoom:50%;" />

<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/nao_trajectory_config.png" alt="nao_trajectory_config" style="zoom:50%;" />

## 4. TESTING

```bash
$ cd 
$ cd nao_virtual2/src/nao_virtual/nao_gazebo_plugin/launch/
$ roslaunch nao_gazebo.launch
```

![nao_running](https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/nao_running.PNG)

### NAO CONTROLLER AND CAMERA TESTING

<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/nao_tutorial/nao_controller_camera.jpg" alt="nao_controller_camera"  />

Success! We are able to see cameras and control joints by ROS Controller interface. Similarly we could do it programatically.

#### A word on NAOQI Driver

If the reader is interested in using NAOQI interface, check http://doc.aldebaran.com/2-4/dev/cpp/newsdk.html to download SDK.
Since is meant to be run in ROS Kinetic, an option is to run from a different computer or virtual machine to interact with NAO, that's not very hard to do.

Or the reader may want to fix the errors with `naoqi driver` and port it to Python 3. I decided that both options are outside of the scope of this tutorial. 
And based on the community discussion, looks there will be a `naoqi driver` compatible with Python 3 will come in the near future, so I decided to go with option 1 and wait for the new version.


