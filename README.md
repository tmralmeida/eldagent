# eldagent
Agent for elderly care. Aiming to apply RL, DL in a turtlebot3

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

After running the previous commands, we are able to run the gmapping node:
```
roslaunch eldagent_bringup gmapping.launch
```

```
roslaunch eldagent_bringup amcl.launch
```