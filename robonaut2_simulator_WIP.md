<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# Robonaut2 Simulator Work In Progress

Not an easy conversion. I will report progress here, but may take me about 2-3 weeks to complete.

## First Attempt:

Found this repo https://github.com/Halbmond/r2_sim. It was a very good starting point to understand structure, and at least how all the pieces work together.
The Last original build was done ROS Indigo, so we are dealing with an older version of Gazebo as well that is not very compatible. First things first, let's compile it.

## 1. Create Workspace

```
$ mkdir -p r2_sim/src
$ cd r2_sim/src
$ git clone -b indigo https://bitbucket.org/nasa_ros_pkg/deprecated_nasa_r2_simulator.git
$ git clone -b indigo https://bitbucket.org/nasa_ros_pkg/deprecated_nasa_r2_common.git
$ cd ..
$ catkin_make
```

Wow! So many errors to fix. Too many to even try to make a tutorial out of it. This document helped a lot: https://github.com/osrf/gazebo/blob/gazebo11/Migration.md
Worked methodically, fixing one error at the time, it was great exercise to understand how the code works, so I believe it was time well spent, but I am sure not many will enjoy it.
So rather I will share the fix files in .zip., you are welcome to compare the codes. 

This exercise took 2 afternoons/nights and lots of coffee. I am sure it's not 100% right, but I got it compiled with no errors.

Once compiled, then it's time to source it and test"

```
$ echo 'source ~/r2_sim/devel/setup.bash'>>~/.bashrc
$ source ~/.bashrc
```

## 2. Testing

```
$ roslaunch r2_gazebo r2_gazebo.launch
```





