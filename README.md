# eldagent
**eldagent** is an agent for elderly care. It aims to interact with older adults in a home scenario.
It is under construction. This repo contains the roadmap throughout this project.

# Table of Contents
- [Pre-Requisites](#pre-requisites)
- [Initial Steps](#initial-steps)
    * [Initial Commands](#initial-commands)
    * [SLAM and Localization commands](#slam-and-localization-commands)



# Pre-Requisites

- [turtlebot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- [ROS-noetic](http://wiki.ros.org/noetic/Installation)
- [Gazebo simulator](http://gazebosim.org/)
- [gmapping SLAM algorithm](http://wiki.ros.org/gmapping)
- [ACML localization algorithm](http://wiki.ros.org/amcl)



# Initial Steps

This section depicts the initial steps of our approach. It states every command line according to the respective task.

## Initial Commands

These initial commands contain the steps to teleoperate an agent in a custom or a default world (from Gazebo). Based on the [ROBOTIS tutorials](https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/), and the launch files from the eldagent_bringup package stems from [turtlebot3_simulations package](https://github.com/ROBOTIS-GIT/turtlebot3_simulations/blob/master/turtlebot3_gazebo/launch/turtlebot3_house.launch).  

1 - Simulator launching:  
```
roslaunch eldagent_bringup bringup_gazebo.launch  
```

2 - Robot spawning:
```
roslaunch eldagent_bringup spawn.launch
```

3 - Rviz custom visualization:
```
roslaunch eldagent_bringup visualize.launch
```

4 - (Optional) Teleoperation:
```
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```


## SLAM and Localization commands

After running the previous commands, we can run the gmapping node:
```
roslaunch eldagent_bringup gmapping.launch
```

```
roslaunch eldagent_bringup amcl.launch
```