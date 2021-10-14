<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# Nao Simulator

The Nao is a commercially available, 60cm tall, humanoid robot targeted at research lab and classrooms. 
The Nao is small, but it packs a lot into its tiny frame: four microphones, two VGA cameras, touch sensors on the head, infrared sensors, and more. 
The use of Nao with ROS has demonstrated how quickly open-source code can enable a community to come together around a common hardware platform.

Most of the documents to make NAO Simulation work dates back to ROS Indigo, so not an easy task to make it work in ROS Noetic.
So the plan is to divide the task in two. First we will get the NAO model to work in Gazebo and communicate with ROS. Then we will connect the `naoqi` driver
to ensure NAO can do programmed functions like walking, etc.

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

_Notice I used `nao_virtual2` for workspace. For some weird reason if I use `nao_virtual` it doesn't source properly after I compiled the `nao_robot` workspace.
_

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

At this point the main error was not able to run as in order to use the NAO meshes, a license needs to be accepted.
To work around this problem, I installed qibullet `pip install qibullet`.

Then to get the meshes properly pointed, I Copied `meshes` folder from `.ros` folder to `nao_meshes_ws/src/nao_meshes/` since `qibullet` installed them in that folder but ROS is looking for `nao_meshes` from `nao_meshes_ws` package.

Next many errors regarding urdf and to fix this was an iterative process, so not sequential. I tried a bit each day, advance on why meshes were not visible, then back to URDF.
Main summary of what needs to be addressed for urdf. I will also make the urdf file available for those interested. 

Important to know is that we are using NaoV40_generated files found at `/nao_robot/src/nao_robot/nao_description/urdf/naoV40_generated_urdf`.

1. Removed warnings by adding `hardware_interface` in `naoTransmission.xacro` file.

```xml
<hardwareInterface>hardware_interface/PositionJointInterface</hardwareInterface>
```

2. `AnklePitch`  **link** name same `AnklePitch` **joint,**  to fix had to change to `AnklePitchJoint` for all the places that apply `nao.urdf` and `naoTranmission.xacro` and `nao_legs.xacro

3. Added zero inertias and very small mass to all links even if they were 'faked' such as `sole` link that connect foot to the floor.

To test the urdf file was good with gazebo:

gz sdf -p nao.urdf

Results so far:

Meshes successfully loaded and tested with: `roslaunch nao_gazebo_plugin nao_gazebo.launch`

![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/Nao_gazebo.PNG)

`roslaunch nao_gazebo_plugin nao_gazebo_plugin_H25.launch`
![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/Nao_soccer_field.PNG)

However, we get an error when trying `roslaunch nao_full.launch`

![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/naoqi_driver_missing.PNG)

More testing required for the NAO sensors so that will be next priority. I will create another progress report for Naoqi driver installation as well and combine both as Nao Simulator tutorial for ROS Noetic.
Unfortunately I obsessed with this project a little and have neglected Robonaut, so will get back to that project after Nao is operational.
