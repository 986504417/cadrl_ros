# cadrl_ros (Collision Avoidance with Deep RL)

ROS implementation of a dynamic obstacle avoidance algorithm trained with Deep RL
<img src="misc/A3C_20agents_0.png" width="500">

#### Paper:

M. Everett, Y. Chen, and J. P. How, "Motion Planning Among Dynamic, Decision-Making Agents with Deep Reinforcement Learning", submitted to IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), 2018
Link: to be added

#### Dependencies:

[TensorFlow](https://www.tensorflow.org/) is required (tested with version 1.4.0). 
[ROS](http://wiki.ros.org/) is required (tested with Kinetic on Ubuntu 16.04)
numpy
For other dependencies, please refer to src/dependencies_install.sh.  

#### To Run:
Clone and build this repo (assume destination is ~/catkin_ws/src)
```
$ cd ~/catkin_ws/src
$ git clone git@github.com/mfe7/cadrl_ros
$ cd ~/catkin_ws && catkin_make
```

Connect inputs/outputs of your system to `launch/cadrl_node.launch`

##### Subscribed Topics:
* ~pose [[geometry_msgs/PoseStamped]](http://docs.ros.org/api/geometry_msgs/html/msg/PoseStamped.html)
	Robot's pose in the global frame

* ~velocity [[geometry_msgs/Vector3]](http://docs.ros.org/kinetic/api/geometry_msgs/html/msg/Vector3.html)
	Robot's linear velocity in the global frame (vx, vy)

* ~goal [[geometry_msgs/PoseStamped]](http://docs.ros.org/api/geometry_msgs/html/msg/PoseStamped.html)
	Robot's goal position in the global frame

* ~clusters [[ford_msgs/Clusters]]()
	Positions, velocities, sizes of other agents in vicinity

* TODO: planner_mode, safe_actions, peds

##### Published Topics:
* ~nn_cmd_vel [[geometry_msgs/Twist]](http://docs.ros.org/api/geometry_msgs/html/msg/Twist.html)
	Robot's commanded twist (linear, angular speed) according to network's output

* The other published topics are just markers for visualization
	* ~pose_marker shows yellow rectangle at position according to ~pose
	* ~path_marker shows red trajectory according to history of ~pose
	* ~goal_path_marker shows blue arrow pointing toward position of commanded velocity 1 second into future
	* ~agent_markers shows orange cylinders at the positions/sizes of nearby agents

* TODO: remove other_agents_marker, other_vels

##### Parameters:
* ~jackal_speed
	Robot's preferred speed (m/s) - tested below 1.2m/s (and trained to be optimized near this speed)

#### Primary code maintainer:
Michael Everett (https://github.com/mfe7)
