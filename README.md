# eldagent
**eldagent** is a social robot for elderly care. It aims to interact with older adults in a home scenario.
This repo is under construction, and it contains the roadmap throughout this project.

# Table of Contents
- [Pre-Requisites](#pre-requisites)
- [Initial Steps](#initial-steps)
    * [Initial Commands](#initial-commands)
    * [SLAM and Localization commands](#slam-and-localization-commands)
    * [Turtlebot2 working on ROS-Noetic](#turtlebot2-working-on-ros-noetic)



# Pre-Requisites

- [turtlebot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- [ROS-noetic](http://wiki.ros.org/noetic/Installation)
- [Gazebo simulator](http://gazebosim.org/)
- [gmapping SLAM algorithm](http://wiki.ros.org/gmapping)
- [ACML localization algorithm](http://wiki.ros.org/amcl)
- Follow [Turtlebot2 instructions](#turtlebot2-working-on-ros-noetic)



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
roslaunch eldagent_bringup spawn_tbot3.launch
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


## Turtlebot2 working on ROS-Noetic

1 - Clone repo of turtlebot2 packages

```
git clone https://github.com/Usama-Arshad16/turtlebot2_navigation
```
2 - Unzip both directories

3 - From these packages, two were removed: robot_pose_ekf and orocos-bayesian-filtering (couldn't find a way of build them from source)

4 - Clone yocs_controllers repo.  

```
git clone https://github.com/yujinrobot/yujin_ocs.git
```

5 - From this package, yocs_ar* were removed to avoid install opencv  

6 - Clone yocs_msgs repo and build it

```
git clone https://github.com/yujinrobot/yocs_msgs
```

```
catkin_make
```

7 - Step 1 from [initial commands](#initial-commands)


8 - Turtlebot2 robot spawning:

```
roslaunch eldagent_bringup spawn_tbot2.launch
```

9 - Try to move it on Gazebo. Any SyntaxError means that the first line of the turtlebot_teleop_key.py should be python3 env. Moreover, in that same script, the name of the topic should become **/cmd_vel**. The robot still doesn't move right? Go to the next step.

```
roslaunch turtlebot_teleop keyboard_teleop.launch
```

10 - We must include a differential driver on turtlebot_gazebo.xacro.urdf, such as:

```
<gazebo>
  <plugin name="turtlebot_controller" filename="libgazebo_ros_diff_drive.so">
    <commandTopic>cmd_vel</commandTopic>
    <odometryTopic>odom</odometryTopic>
    <odometryFrame>odom</odometryFrame>
    <odometrySource>world</odometrySource>
    <publishOdomTF>true</publishOdomTF>
    <robotBaseFrame>base_footprint</robotBaseFrame>
    <publishWheelTF>false</publishWheelTF>
    <publishTf>true</publishTf>
    <publishWheelJointState>true</publishWheelJointState>
    <legacyMode>false</legacyMode>
    <updateRate>30</updateRate>
    <leftJoint>wheel_left_joint</leftJoint>
    <rightJoint>wheel_right_joint</rightJoint>
    <wheelSeparation>0.287</wheelSeparation>
    <wheelDiameter>0.066</wheelDiameter>
    <wheelAcceleration>1</wheelAcceleration>
    <wheelTorque>10</wheelTorque>
    <rosDebugLevel>na</rosDebugLevel>
  </plugin>
</gazebo>
```

11 - Repeat the teleop launching and everything should work.

```
roslaunch turtlebot_teleop keyboard_teleop.launch
```
