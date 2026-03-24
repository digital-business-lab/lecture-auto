# Session 9 — SLAM, Navigation & TurtleBot3 Workflow

**Duration: 3 hours · Not graded**

---

## Goal

By the end of this session you will be able to:

- [ ] Execute the complete TurtleBot3 autonomous navigation workflow from bring-up to goal navigation
- [ ] Explain the difference between the mapping phase (SLAM) and the navigation phase (AMCL)
- [ ] Describe what each step of the workflow achieves and which ROS nodes are involved
- [ ] Interpret the visualisations in RViz: occupancy grid, particle cloud, planned path
- [ ] Name concrete differences between simulation and real-hardware behaviour

---

## The TurtleBot3 Workflow

This session follows a fixed five-step sequence. Each step builds on the previous one — do not skip steps.

```
[1. Bring-Up]
     │
     ▼
[2. Teleoperation] ──► [3. SLAM Mapping] ──► [4. Save Map]
                                                    │
                                                    ▼
                                         [5. Autonomous Navigation]
                                         (AMCL + move_base)
```

Steps 1–4 produce a map. Step 5 requires that map to navigate autonomously.

---

## Step 1 — Bring-Up

Launch the TurtleBot3 simulation. This starts all required nodes: the robot model, simulated LiDAR, odometry, and the ROS parameter server.

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

Open RViz in a second terminal using the pre-configured profile provided by your lecturer.

!!! question "Observe"
    Run `rosnode list`. Which nodes are now active? Compare with your notes from Session 8.

---

## Step 2 — Teleoperation

Drive the robot manually using keyboard input. This sends velocity commands on the `/cmd_vel` topic.

```bash
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```

| Key | Action |
|---|---|
| `i` | Drive forward |
| `,` | Drive backward |
| `j` / `l` | Rotate left / right |
| `k` | Stop |

!!! question "Observe"
    Drive the robot in a rough square. Does it return exactly to its starting position? Open `rostopic echo /odom` in a second terminal and watch the position values as you drive. What do you notice?

---

## Step 3 — SLAM Mapping

Launch `gmapping`. The SLAM node subscribes to `/scan` and `/odom` and begins building an occupancy grid map as you drive.

```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```

In RViz you will see the map grow in real time:

| Colour | Meaning |
|---|---|
| White | Free space — confirmed passable |
| Black | Obstacle — wall or object detected |
| Grey | Unknown — not yet explored |

Drive slowly through the **entire world**, covering all corridors and rooms. The map should be complete (no large grey areas) before you proceed to Step 4.

!!! warning "Drive slowly"
    Driving too fast degrades map quality. The LiDAR needs time to build up a consistent scan at each position. If the map looks distorted, slow down.

!!! question "Observe"
    What happens to the map if you revisit an area you have already mapped? Does the map update or stay the same?

---

## Step 4 — Save the Map

Export the finished map before shutting down the SLAM node. This creates two files in your home directory.

```bash
rosrun map_server map_saver -f ~/map
```

| File | Content |
|---|---|
| `map.pgm` | The occupancy grid as a grayscale image |
| `map.yaml` | Metadata: resolution, origin, threshold values |

!!! question "Observe"
    Open `map.pgm` in an image viewer. Does it match what you saw in RViz? Open `map.yaml` and read it — what does the `resolution` field tell you?

Now **shut down the SLAM launch file** (Ctrl+C in that terminal) before continuing.

---

## Step 5 — Autonomous Navigation

Load the saved map and start the navigation stack. This launches AMCL (localisation on the known map) and `move_base` (path planning and execution).

```bash
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```

### Set the initial pose

The robot does not yet know where it is on the map. Tell it approximately:

1. In RViz, click **"2D Pose Estimate"** in the toolbar.
2. Click on the map at the robot's approximate position and drag to indicate its heading.
3. The particle cloud appears — initially spread out (high uncertainty).
4. Drive the robot a short distance with `teleop_twist_keyboard`. Watch the particle cloud narrow as AMCL converges.

### Send a navigation goal

1. In RViz, click **"2D Nav Goal"** in the toolbar.
2. Click a target position on the map and drag to set the arrival heading.
3. The global planner draws the intended path (green line).
4. The robot drives autonomously to the goal, adjusting for obstacles with the local planner.

!!! question "Observe"
    - How does the planned path (green line) change while the robot is moving?
    - What happens if you place a virtual obstacle in the robot's path in Gazebo?
    - Where in this workflow does the Dijkstra / A* algorithm run?
    - What is the difference between what `gmapping` did in Step 3 and what AMCL does in Step 5?

---

## Tips

!!! tip "If the robot gets stuck"
    The local planner will try to replan automatically. If the robot stops for more than ~10 seconds, send a new navigation goal from a different position, or use `teleop_twist_keyboard` to manually move it out of the stuck position.

!!! tip "If the map does not load"
    Make sure the SLAM launch file from Step 3 is fully shut down before starting Step 5. Two instances of the map server conflict with each other.

!!! tip "Fallback map"
    If your mapping run was incomplete or distorted, a pre-built fallback map is available in the `scripts/` folder. Ask your lecturer for the path.
