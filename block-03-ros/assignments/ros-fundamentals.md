# ROS Fundamentals Activity Sheet

## Objective
Explore the basics of ROS Noetic environment using TurtleBot3 simulation.

## Setup
Pre-configured VMs with ROS Noetic + TurtleBot3 simulation packages installed.

## Activity Steps

### Step 1: Launch TurtleBot3 Gazebo Simulation
Open a terminal and run:
```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

### Step 2: Launch RViz for Visualization
Open a second terminal and run:
```bash
rviz
```

### Step 3: Run rqt_graph
In a third terminal, run:
```bash
rqt_graph
```
Sketch the node–topic graph here:

### Step 4: List Active Topics
In a fourth terminal, run:
```bash
rostopic list
```
Active topics:
- `/cmd_vel`
- `/depth/image`
- `/depth/image_raw`
- `/depth/points`
- `/imu`
- `/joint_states`
- `/laser/scan`
- `/map`
- `/map_metadata`
- `/odom`
- `/rosout`
- `/scan`
- `/tf`
- `/tf_static`
- `/turtlebot3/gazebo/odom`
- `/turtlebot3/gazebo/scan`

### Step 5: Examine LiDAR Data
In a fifth terminal, run for 10 seconds:
```bash
rostopic echo /scan
```
Structure and value range of laser data:
- `header`: timestamp and frame_id
- `angle_min`: -2.3518 radians (-135°)
- `angle_max`: 2.3562 radians (135°)
- `angle_increment`: 0.0044 radians (~0.25°)
- `time_increment`: 0.0 seconds
- `scan_time`: 0.0333 seconds (30 Hz)
- `range_min`: 0.12 meters
- `range_max`: 3.0 meters
- `ranges`: Array of distance measurements (1081 values)
- `intensities`: Array of intensity values (1081 values)

### Step 6: Examine Odometry Data
In a sixth terminal, run:
```bash
rostopic echo /odom
```
Structure comparison to LiDAR data:
- `header`: timestamp and frame_id
- `child_frame_id`: "base_footprint"
- `pose`: Position (x, y, z) and Orientation (x, y, z, w)
- `twist`: Linear velocity (x, y, z) and Angular velocity (x, y, z)

## Reflection Questions

### Question 1
Which node publishes `/scan`? Which subscribes?

**Answer:** 
The `/scan` topic is published by the LiDAR sensor node (typically `turtlebot3_lidar` or similar), and it's subscribed to by various nodes that need to process the laser scan data for navigation, obstacle detection, etc.

### Question 2
What would happen if the LiDAR node crashed?

**Answer:**
If the LiDAR node crashed:
- The `/scan` topic would stop publishing
- Any nodes that depend on laser scan data (like navigation algorithms, obstacle avoidance, SLAM) would lose their sensor input
- The robot's ability to perceive its environment would be severely compromised
- The system might fail to detect obstacles or navigate safely

### Question 3
Name two topics you would need to monitor to understand if the robot is moving.

**Answer:**
1. `/odom` - Provides odometry data including position and velocity information
2. `/cmd_vel` - Shows the commanded velocities that are being sent to the robot's motors

## Additional Commands
Useful additional commands for exploration:
```bash
# View topic details
rostopic info /scan

# Monitor topic frequency
rostopic hz /scan

# View message type and structure
rostopic type /scan

# Get topic statistics
rostopic stats /scan
```
