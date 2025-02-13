# AMP Autonomous Software Stack v2

Second iteration of the Autonomous Software Stack (ASS) for the AMP go-kart.

# Current Nodes
## stage_ros
See sim\_files inside the `env_sim` file for the image file that specifies the shape of the racetrack and the config files that define the simulated laserscanner sensor and kart.

This simulated kart takes /cmd\_vel topic to move. (cmd\_vel contains tf map frame, quaternion, and 3d pose, but we are only using it for forward displacement and yaw displacement)   

Broadcasts /top/scan, which is the current moment laserscan data as a list of each ray's distance in a 180 degree range. 

## slam_mode_goal
Reads top/scan and moves the kart towards open space (path finding). Puts out /amp\_slam\_goal which is a MoveBaseGoal structure that represents displacement. TODO: change from MoveBaseGoal to something simpler.

slam\_mode\_goal is intended to put out high-level, ideal cart commands that are translated by the mover node into hardware commands for the kart's motors and steering.

## Mover
Takes MoveBaseGoal and converts them to cmd_vel to the simulated kart

# Running 
* Show available options help
```
. amd64-docker.sh 0
```

To build the docker image, have a second argument behind the number.
* Run intel graphics docker
```
. amd64-docker.sh 1
```
* Run nvidia graphics docker
```
. amd64-docker.sh 2
```
