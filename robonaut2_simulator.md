<img src="https://github.com/robogeekcanada/noetic_robots/blob/main/images/RG-logo.jpg" alt="alt text" width=100 height=150>

[@robogeekcanada](https://robo-geek.ca/)

# Robonaut 2 Simulator

The Robonaut project has been conducting research in robotics technology on board the International Space Station (ISS) since 2012 (more on R2 in the ISS). Recently, the original upper body humanoid robot was upgraded by the addition of two climbing manipulators ("legs"), more capable processors, and new sensors.
Source: https://robonaut.jsc.nasa.gov/R2/

Robonaut 2 Simulator NASA public version has been deprecated and the las build done was in ROS Indigo. So to run in ROS Noetic there were many challenges.
As discussed in the progress report, the first attempt was to work all the issues from the NASA repo. This partially worked, but not an easy task.
Then I stopped decided to see if I could code the Simulator code separately but this was also not an easy task. As I was working on the conversion, I found that the majority of the issues were with macros, so I decided to remove them and even though this resulted in longer urdf files, it made troubleshooting manageable.

Therefore, I decided to go back and finish converting NASA depecrated repo and was able to get most functionality working.

I shared this progress with one of the leaders of this project, and found to my great surprise a public version that works with ROS Noetic from TracLabs:

https://bitbucket.org/traclabs/nasa_r2_simulator 

https://bitbucket.org/traclabs/nasa_r2_common

Not all functionality works with the above repo but it will get you started. 

As for the repo I converted, I will share the results for now, but until I get some sort of permission from the original owners I won't share the changes. Problem  is licensing is not clear and I am very respectful of the great work done by Robonaut 2 team so I want to do things right.

## Results

![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/Gazebo%20camera%20and%20joint%20control.jpg)

![image](https://github.com/robogeekcanada/noetic_robots/blob/main/images/Robonaut_animation%20RG%20RN%20logo.gif)

 


