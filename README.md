# Semantic-arena
This repository provides a platform to develop semantic drl based navigation approaches. It uses to arena-rosnav repository and combines it with pedsim for human behavior modeling. Furthermore it extends the pedisim social force model with industrial object classes like forklift, vehicle or collaborative robots. 
The repository also provides 3 semantic drl-based agents which are able to navigate savely around different human types.


# Pedestrian Simulator
Pedestrian Simulator (Pedsim) is a 2D pedestrian simulator based on the social force model of Helbing et. al. Note the original repository: https://github.com/srl-freiburg/pedsim_ros

Movement of the agents in the simulation is mostly controlled by three forces:
- desired force (pulls agent towards the current destination)
- social force (pushes agent away from other agents)
- obstacle force (pushes agent away from obstacles)

Additionally agents can perform different actions that interrupt or modify the movement like talking to each other, stand as a group or take a walk with another agent.
We also implemented the possibility to spawn a forklift agent that has the same basic movement functionality but has different actions e.g. loading/unloading objects.

For Pedsim to work together with Arena-Rosnav it needs to be synced to Flatland Simulator. This is done via a flatland plugin that subscribes to the **simulated_agents** topic published by Pedsim and updates the position of the corresponding flatland models accordingly.

## Examples

| <img width="400" height="250" src="/img/pedsim/takingawalk.gif"> | <img width="400" height="250" src="/img/pedsim/grouping.gif"> | 
|:--:|:--:|
| *Human agents walking together* | *Human agents standing as a group* |

| <img width="400" height="250" src="/img/pedsim/forklift.gif"> | 
|:--:|
| *Forklift agent doing some work* |


# Demo
#### 1. Normal Arena-Rosnav Installation
See [Installation Manual](https://github.com/ignc-research/semantic-arena/blob/main/docs/Installation.md)

#### 2. Switch to sim_to_real branch and pull forks
```
cd ~/catkin_ws/src/arena-rosnav
git checkout sim_to_real
rosws update --delete-changed-uris .
```

#### 3. Build and Source
```
cd ~/catkin_ws
catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3
source devel/setup.zsh
```

#### 4. Start Demo
```
workon rosnav
roslaunch arena_bringup pedsim_demo.launch
```
This will start Flatland, Pedsim and a script that will spawn a few agents.
