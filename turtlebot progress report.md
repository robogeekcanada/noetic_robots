<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# Turtlebot





## 1. Installation from Source

```bash
$ mkdir -p turtlebot_ws/src
$ cd turtlebot_ws/src
$ git clone https://github.com/turtlebot/turtlebot_msgs.git
$ git clone https://github.com/turtlebot/turtlebot.git
$ git clone https://github.com/turtlebot/turtlebot_simulator.git
$ git clonehttps://github.com/turtlebot/turtlebot_apps.git
$ cd ..
$ catkin_make

$ echo 'source ~/turtlebot_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

## 2. Dependencies for laser, kobuki description and mobility

```bash
$ mkdir -p kobuki_ws/src
$ cd kobuki_ws/src
$ git clone https://github.com/yujinrobot/kobuki_description.githttps://github.com/yujinrobot/kobuki.$ git clone https://github.com/yujinrobot/kobuki_msgs.git
$ git clone https://github.com/yujinrobot/kobuki_core.git
$ cd ..
$ catkin_make

$ echo 'source ~/kobuki_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

```bash
$ mkdir -p cmd_vel_mux/src
$ cd cmd_vel_mux/src
$ git clone https://github.com/bangyii/cmd_vel_mux.git
$ cd ..
$ catkin_make

$ echo 'source ~/cmd_vel_mux/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

```bash
$ sudo apt-get install ros-noetic-ecl-exceptions
$ sudo apt-get install ros-noetic-ecl-time
$ sudo apt-get install ros-noetic-ecl-core
$ sudo apt-get install ros-noetic-ecl-console
$ sudo apt install ros-noetic-depthimage-to-laserscan -y
$ sudo apt-get install ros-noetic-ecl-mobile-robot
$ sudo apt-get install libusb-dev
$ sudo apt-get install libftdi-dev
```

```bash
$ mkdir -p yocs_ws/src
$ cd yocs_ws/src
$ git clone https://github.com/yujinrobot/yujin_ocs.git
$ git clone https://github.com/yujinrobot/yocs_msgs.git
$ git clone https://github.com/ros-perception/ar_track_alvar.git
$ git clone -b noetic-devel $ git clone https://github.com/machinekoder/ar_track_alvar.git -b noetic-devel
$ cd ..
$ catkin_make

$ echo 'source ~/yocs_ws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### Rviz dependencies

```bash
$ mkdir -p turtlebot_viz/src
$ cd turtlebot_viz/src
$ git clone https://github.com/turtlebot/turtlebot_viz.git
$ cd ..
$ catkin_make
$ echo 'source ~/turtlebot_viz/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

Successful compilation. 


## Testing

```bash
$ rqt_graph
```

![image-20211026134105971](https://github.com/robogeekcanada/noetic_robots/blob/main/images/turtlebot_images/rqt_graph.png)


## [ubuntu 20.04 "rosrun tf view_frames" failed to run]

```bash
$ rosrun tf view_frames
```

Report an error

```bash
1 Listening to /tf for  5.0 seconds
 2  Done Listening
 3 b ' dot-graphviz version 2.42.3 (0)\n ' 
4  Traceback (most recent call last):
 5    File " /opt/ros/melodic/lib/tf/ view_frames " , line 119 , in <module>
 6      generate(dot_graph)
 7    File " /opt/ros/melodic/lib/tf/view_frames " , line 89 , in generate
 8      m = r.search(vstr)
 9TypeError: cannot use a string pattern on a bytes-like object
```

### Solution


```bash
1 $ sudo vim /opt/ros/noetic/lib/tf/view_frames 
```

 Then open the VIM editor to modify the code

```python
m = r.search(vstr.decode( ' utf-8 ' ))
```

```bash
$ rosrun tf view_frames
```

![image-20211026134321933](https://github.com/robogeekcanada/noetic_robots/blob/main/images/turtlebot_images/view_frames.png)

### teleop

Not working due navigation stack did pub. topic on `/cmd_vel_mux`sometimes, rviz control robot base by topic `/cmd_vel`

### RViz launch files
Need some work, not fully functioning

