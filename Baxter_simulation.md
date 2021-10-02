<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# Baxter Simulator installation

## 1. Dependencies
```bash
$ sudo apt-get install ros-noetic-effort-controllers
```

## 2. Installation
```bash
$ cd
$ mkdir -p baxterws/src
$ cd baxterws/src/
$ wstool init
$ wstool merge https://gist.githubusercontent.com/jarvisschultz/f65d36e3f99d94a6c3d9900fa01ee72e/raw/baxter_packages.rosinstall
$ wstool update
$ source /opt/ros/noetic/setup.bash
$ cd ..
$ catkin_make
# Refer to Troubleshooting, to fix couple files if catkin_make fails.
$ echo 'source ~/baxterws/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

### 3. Troubleshooting

* Error exception in robot_enable.py:
  * Remove CV_LOAD_IMAGE_UNCHANGED
    `~/baxterws/src/baxter_simulator/baxter_sim_hardware/src/baxter_emulator.cpp`

## 4. Testing

Check if packages were installed, if not make sure the package is properly built

T1:
```bash
$ rospack list
```

T2:
```bash
$ roslaunch baxter_sim_examples baxter_pick_and_place_demo.launch
```

Partially working...need to fix some stuff

To be tested....
T3: 
```bash
$ rosrun intera_examples camera_display.py
```
![Baxter simulator](https://github.com/robogeekcanada/noetic_robots/blob/main/images/Baxter%20simulator.PNG)

### Options to be tested:

```bash
$ rosrun intera_examples camera_display.py -c head_camera
$ rosrun intera_examples camera_display.py -c right_hand_camera
$ rosrun intera_examples camera_display.py -e
```

Once Baxter is working well, I will try to work on Sawyer as it should be similar fixes.
