# Session 9 — AGV Technology & ROS Fundamentals

**Duration: 3 hours · Not graded**

---

## Goal

By the end of this session you will be able to:

- [ ] Name the main sensor types used in autonomous AGVs and describe what each one measures
- [ ] Explain why dead reckoning alone is not sufficient for precise navigation
- [ ] Describe how landmark-based localisation (e.g. AprilTags) corrects position drift
- [ ] Explain the particle filter idea behind AMCL in your own words
- [ ] Distinguish the roles of global planner and local planner in ROS
- [ ] Describe the ROS concepts node, topic, and message using your own examples
- [ ] Run basic ROS commands and interpret their output

---

## Part 1 — Autonomous AGV Technology

The lecture introduces the technical building blocks that make autonomous navigation possible. The corresponding slides are available on Moodle. The key concepts are summarised below for reference.

### Sensors

An AGV without reliable perception cannot navigate safely. The table below lists the main sensor types found on modern autonomous vehicles:

| Sensor | What it measures | Typical role | Key limitation |
|---|---|---|---|
| **LiDAR** | Distance to obstacles, 360° point cloud | Obstacle detection, SLAM, localisation | Expensive; glass and mirrors cause artefacts |
| **Camera** | Visual image | AprilTag detection, visual SLAM | Sensitive to lighting; computationally expensive |
| **IMU** | Acceleration, angular velocity | Orientation estimation, drift correction | Accumulates error over time |
| **Wheel encoders** | Wheel rotation count | Odometry (dead reckoning) | Slip leads to cumulative position error |
| **Ultrasonic** | Close-range distance | Safety stop zone detection | Low resolution; slow update rate |

The TurtleBot3 used in this course is equipped with a 360° LiDAR and wheel encoders.

### Dead Reckoning

Dead reckoning estimates the robot's position purely from its starting point and movement data (wheel rotations, speed, direction). No external reference is needed — but errors accumulate with every step, and the estimate drifts further from reality over time.

**Key insight:** Dead reckoning alone is not sufficient for long-distance navigation. A correction mechanism is required.

### Landmark-Based Localisation

Known fixed points in the environment can correct position drift. This course uses **AprilTags** — printed black-and-white square markers that a camera can detect and use to compute the robot's precise distance and orientation.

!!! info "AprilTags in the lab"
    In the course lab, AprilTags are mounted at known positions on the walls. When the robot's camera detects a tag, it immediately knows where it is relative to that tag — and therefore in the entire room. This provides accurate, drift-free localisation without any map-building.

### Probabilistic Localisation — AMCL

Rather than maintaining a single position estimate, the robot keeps *hundreds of hypotheses* (particles) about where it might be. Each particle represents one possible position and orientation.

1. **Initialisation** — Particles are spread across the entire map (unknown start) or in a cluster (known approximate start).
2. **Motion update** — Every time the robot moves, all particles shift accordingly — plus a small random noise to model imperfection.
3. **Sensor update** — Each particle is scored by how well the expected LiDAR scan from that position matches the actual scan. Particles in wrong positions get low scores.
4. **Resampling** — Low-scoring particles are dropped; high-scoring particles multiply. The cloud converges to the robot's true location.

**Key insight:** The robot is never *certain* of its position — it holds a probability distribution. As it moves and perceives, that distribution narrows.

### Path Planning

Once the robot knows where it is, it needs to decide how to reach a goal. ROS splits this into two layers:

| Layer | Role | Re-computed |
|---|---|---|
| **Global planner** (Dijkstra / A*) | Finds the optimal route through the full map | Once per goal |
| **Local planner** (DWA) | Executes the route in real time, avoiding dynamic obstacles | ~10 times per second |

The **Dijkstra algorithm** builds the globally shortest path by expanding outward from the start node, always visiting the lowest-cost unvisited node next. A worked example is provided in the lecture slides on Moodle.

### SLAM — Simultaneous Localisation and Mapping

SLAM solves the chicken-and-egg problem of autonomous navigation: to localise, you need a map; to build a map, you need to know where you are. SLAM does both at the same time as the robot drives through an unknown environment, producing an **occupancy grid map** — a 2D grid where each cell is marked as free, occupied, or unknown.

In this course, the `gmapping` package is used.

---

## Part 2 — ROS Architecture

ROS (Robot Operating System) is the middleware standard for modern robotics. It provides hardware abstraction, modular communication, and thousands of reusable packages.

### Core Concepts

| Concept | What it is | Example |
|---|---|---|
| **Node** | An independent process that does one job | The LiDAR driver node |
| **Topic** | A named data channel; nodes publish or subscribe | `/scan` carries LiDAR data |
| **Message** | The data type carried on a topic | `sensor_msgs/LaserScan` |
| **Service** | Synchronous request–response call | Request map from map server |
| **Action** | Long-running task with progress feedback | Drive to a goal position |

### Key Packages Used in This Course

| Package | Role |
|---|---|
| **Gazebo** | 3D physics simulator — runs the virtual TurtleBot3 |
| **RViz** | Visualises sensor data, particle cloud, map, planned path |
| **Navigation Stack** | Integrates AMCL and `move_base` for autonomous navigation |
| **gmapping** | SLAM: builds the occupancy grid map from LiDAR data |
| **teleop_twist_keyboard** | Keyboard teleoperation — sends `/cmd_vel` commands |
| **rqt_graph** | Displays the live node–topic graph of the running system |

---

## Part 3 — Activity: First ROS Environment

You work on the pre-configured VM. All required packages are installed.

### Setup

Launch the TurtleBot3 Gazebo simulation:

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

Open a second terminal and launch RViz to visualise the simulation. A pre-configured RViz profile is provided — ask your lecturer.

### Tasks

Work through the following steps and note your observations on the activity sheet.

**1. Inspect the running system**

```bash
rosnode list
rostopic list
```

Note: How many nodes are running? Which topics do you recognise from the lecture?

**2. Inspect the node–topic graph**

```bash
rqt_graph
```

Sketch the graph on your activity sheet: which nodes publish to which topics?

**3. Read LiDAR data**

```bash
rostopic echo /scan
```

Watch the output for ~10 seconds, then press `Ctrl+C`.

!!! question "Reflection"
    - What values do you see? What unit are the distances in?
    - What happens to the values when you place an object in front of the simulated robot in Gazebo?

**4. Read odometry data**

```bash
rostopic echo /odom
```

!!! question "Reflection"
    - How does the structure of `/odom` differ from `/scan`?
    - Which fields change when the robot moves? Which stay constant?

**5. Drive the robot manually**

```bash
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```

Drive the robot and observe `/odom` in a second terminal.

!!! question "Reflection"
    - Which node publishes `/scan`? Which node subscribes to it?
    - What would happen if the LiDAR node crashed while the robot was navigating?
    - Name two topics you would monitor to understand whether the robot is moving.

!!! tip "Keep your notes"
    Your activity sheet from this session is your reference for Session 10. Bring it.
