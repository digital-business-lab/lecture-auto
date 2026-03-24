# Session 9 — AGV Technology & ROS Fundamentals

> **Duration:** 3 h · **Graded:** No

**Goal:** Students understand the technical building blocks that make autonomous navigation possible (sensors, localisation, path planning, SLAM) and can describe the ROS architecture using the correct vocabulary. The session ends with hands-on exposure to a live ROS environment.

---

## Agenda Overview

| Time | Phase | Format |
|---|---|---|
| 0:00 – 1:15 | Part 1: Autonomous AGV Technology | Lecturer presentation |
| 1:15 – 1:45 | Part 2: ROS — Architecture and Key Packages | Lecturer presentation |
| 1:45 – 2:00 | Part 3: Live Demo — TurtleBot3 Sensor Data in RViz | Lecturer hardware demo |
| 2:00 – 3:00 | Part 4: Guided Student Activity — First ROS Environment | Individual / pair work |

---

## Part 1 — Autonomous AGV Technology (75 min)

### 1.1 Sensors (15 min)

Why sensors matter: an AGV without reliable perception cannot navigate safely. Overview of the main sensor types used in autonomous systems:

| Sensor | Measured quantity | Typical use on AGV | Limitations |
|---|---|---|---|
| **LiDAR** (laser scanner) | Distance to obstacles, 360° point cloud | Obstacle detection, SLAM, localisation | Expensive; glass/mirrors cause artefacts |
| **Camera** | Visual image | Landmark recognition, AprilTags, visual SLAM | Sensitive to lighting; computationally expensive |
| **IMU** (inertial measurement unit) | Acceleration, angular velocity | Orientation estimation, dead reckoning correction | Drift over time |
| **Wheel encoders** | Wheel rotation count | Odometry (dead reckoning) | Slip leads to cumulative error |
| **Ultrasonic** | Distance (close range) | Safety/stop zone detection | Low resolution; slow update rate |

**Teaching note:** Show a photo of a real AGV with labelled sensors. Turtlebot3 Burger uses a 360° LiDAR (LDS-01) and wheel encoders — connect to the live demo later.

---

### 1.2 Dead Reckoning — Koppelnavigation (10 min)

**Idea:** Estimate current position purely from the starting point and movement data (wheel rotations, speed, direction). No external reference required.

**How it works:**
- Wheel encoders measure how far each wheel has turned
- From wheel rotations → calculate distance travelled and change in heading
- Accumulate these incremental steps to estimate the current pose (x, y, θ)

**Problem:** Every measurement has a small error. Errors accumulate with every step → the position estimate drifts further and further from reality over time. Dead reckoning alone is not sufficient for long-distance or high-accuracy navigation.

**Transition:** We need a way to correct the drift. This is where external references come in.

---

### 1.3 Landmark-Based Localisation — Peilen (10 min)

**Idea:** Use known features in the environment to correct the position estimate.

| Method | Landmark type | How it works |
|---|---|---|
| **Reflector targets** | Passive reflectors mounted at fixed positions | LiDAR detects reflectors and triangulates position |
| **AprilTags** | Printed fiducial markers (like QR codes) | Camera identifies tag ID and computes distance/angle |
| **Natural landmarks** | Distinctive corners, columns, structures | SLAM algorithms extract features without markers |
| **GPS** | Satellite signal | Works outdoors; unusable indoors |

**Teaching note:** Show an AprilTag. Explain that the robot knows the exact position of each tag in the environment map → it can compute its own position when it sees one.

---

### 1.4 Probabilistic Localisation (15 min)

**Problem with hard position estimates:** A single position estimate is fragile — one bad sensor reading can throw it off entirely.

**AMCL — Adaptive Monte Carlo Localisation (particle filter):**

The robot maintains hundreds of *hypotheses* (particles) about where it might be. Each particle represents one possible pose (x, y, θ).

1. **Initialisation:** Particles spread randomly across the whole map (or in a Gaussian cloud if rough starting position is known).
2. **Motion update:** When the robot moves, all particles move the same amount — plus random noise to model uncertainty.
3. **Sensor update:** Each particle is scored by how well its predicted sensor readings match the actual LiDAR scan. Particles in wrong positions get low scores.
4. **Resampling:** Low-scoring particles are discarded; high-scoring particles are duplicated. The cloud converges to the robot's actual location.

**Key intuition for students:** The robot is not certain about its position — it has a *probability distribution* over all possible positions. As it moves and perceives, the distribution narrows.

**Teaching note:** An animation or sequence of four diagrams (random → spread → focused cloud → narrow peak) communicates this far better than equations. Use slide with particle cloud visualisation from RViz.

---

### 1.5 Path Planning (20 min)

**Context:** The robot knows where it is (localisation). It needs to decide *how to get* to a goal position. This is the job of the path planner.

**Two layers in ROS Navigation Stack:**

| Layer | Role | Algorithm examples |
|---|---|---|
| **Global planner** | Finds an optimal path through the known map | Dijkstra, A* |
| **Local planner** | Executes the path while avoiding dynamic obstacles | DWA (Dynamic Window Approach) |

#### Dijkstra Algorithm — Worked Example

> **Note to lecturer:** Insert the prepared worked example here (graph with 6–8 nodes, edge weights representing travel distances or times). Walk through the algorithm step by step:
> 1. Assign distance ∞ to all nodes except start (distance 0)
> 2. Visit the unvisited node with the lowest current distance
> 3. Update distances to its neighbours if a shorter path is found
> 4. Mark node as visited; repeat until goal is reached
> 5. Trace back the shortest path

<!-- TODO: Replace this block with the Dijkstra worked example provided by the lecturer -->
<!-- The example should show: graph diagram, step-by-step table, highlighted shortest path -->

**Connection to practice:** In ROS, the global planner runs Dijkstra (or A*) on the occupancy grid map. Each cell is a node; edge weights reflect traversability (free space costs less than near-obstacle space).

---

### 1.6 SLAM — Simultaneous Localisation and Mapping (5 min)

**The chicken-and-egg problem of autonomous navigation:**
- To localise, the robot needs a map.
- To build a map, the robot needs to know where it is.

**SLAM solves both at the same time** while the robot drives through an unknown environment.

**Output:** An *occupancy grid map* — a 2D grid where each cell is marked as free, occupied, or unknown. This map is then used by the navigation stack for path planning.

**ROS implementations:** `gmapping` (particle-filter based, established), `cartographer` (graph-based, more accurate). In this course we use `gmapping` with TurtleBot3.

---

## Part 2 — ROS: Architecture and Key Packages (30 min)

### 2.1 Why ROS? (5 min)

Without ROS, each robotics project would re-implement the same low-level components (sensor drivers, communication, coordinate transforms) from scratch. ROS provides:

- **Hardware abstraction:** swap a sensor without rewriting the application code
- **Modularity:** each capability runs as an independent process (node)
- **Reusability:** thousands of open-source packages for navigation, vision, manipulation
- **Community:** de-facto standard in research and increasingly in industry

### 2.2 Core Architecture (15 min)

| Concept | What it is | Analogy |
|---|---|---|
| **Node** | An independent process that does one job | A department in a company |
| **Topic** | A named data channel; nodes publish or subscribe | A radio frequency |
| **Message** | The data type carried on a topic (e.g. `sensor_msgs/LaserScan`) | The format of a broadcast |
| **Service** | Synchronous request–response call between nodes | A phone call (you wait for the answer) |
| **Action** | Like a service, but for long-running tasks with feedback | A project with status updates |
| **Parameter server** | Stores configuration values accessible to all nodes | A shared config file |

**Example for TurtleBot3:**
- `/scan` topic: LiDAR node publishes laser scan data → SLAM node subscribes
- `/cmd_vel` topic: teleop node publishes velocity commands → drive controller subscribes
- `/odom` topic: wheel encoder node publishes odometry → navigation stack subscribes

### 2.3 Key Packages and Tools (10 min)

| Package / Tool | Role in this course |
|---|---|
| **Gazebo** | 3D physics simulator — runs the virtual TurtleBot3 |
| **RViz** | Visualises sensor data, the particle cloud, the map, and the planned path |
| **Navigation Stack** | Integrates AMCL, `move_base`, costmaps into autonomous navigation |
| **gmapping** | SLAM: builds the occupancy grid map from LiDAR data |
| **teleop\_twist\_keyboard** | Keyboard-controlled teleoperation — sends `/cmd_vel` commands |
| **rqt\_graph** | Shows the node–topic graph of the running ROS system |
| **rostopic echo** | Prints live messages on any topic to the terminal |

---

## Part 3 — Live Demo: TurtleBot3 Sensor Data in RViz (15 min)

**Hardware:** Real TurtleBot3 (Burger or Waffle Pi), connected to lecturer laptop via Wi-Fi.

**Demo steps:**

1. Launch TurtleBot3 bringup on the robot and the visualisation on the laptop
2. Open RViz — show the LiDAR point cloud rotating in real time
3. Open a terminal, run `rostopic echo /scan` — show raw distance data scrolling
4. Run `rqt_graph` — show the live node–topic graph
5. Drive the robot manually (`teleop_twist_keyboard`) — show `/cmd_vel` messages and how they reach the motor controller node
6. Point out: all of this is exactly what students will see in the Gazebo simulation next

---

## Part 4 — Guided Student Activity: First ROS Environment (60 min)

**Setup:** Pre-configured VMs with ROS Noetic + TurtleBot3 simulation packages installed.

**Activity sheet:** `assignments/ros-fundamentals.md` (→ AP5)

**Steps students follow:**

1. Launch the TurtleBot3 Gazebo simulation using the provided command (`roslaunch turtlebot3_gazebo turtlebot3_world.launch`)
2. Open a second terminal; launch RViz to visualise the simulation
3. Run `rqt_graph` — sketch the node–topic graph in the activity sheet
4. Run `rostopic list` — note all active topics
5. Run `rostopic echo /scan` for 10 seconds — note the structure and value range of the laser data
6. Run `rostopic echo /odom` — compare the structure to the LiDAR data
7. Answer reflection questions in the activity sheet:
   - Which node publishes `/scan`? Which subscribes?
   - What would happen if the LiDAR node crashed?
   - Name two topics you would need to monitor to understand if the robot is moving

**Deliverable:** None (ungraded). Completed activity sheet is kept as reference for Session 10.

---

## Files

| File | Description | Status |
|---|---|---|
| `assignments/ros-fundamentals.md` | Guided activity sheet for students | ⏳ To do (AP5) |
| `scripts/` | Launch file wrappers and README for VM setup | ⏳ To do (AP5) |

---

## Preparation Checklist (Lecturer)

- [ ] TurtleBot3 (real) charged and tested — bringup runs without errors
- [ ] Lecturer laptop: ROS installed, TurtleBot3 packages, RViz profile saved
- [ ] Student VMs: ROS Noetic + TurtleBot3 simulation packages pre-installed and tested
- [ ] Gazebo simulation launches within acceptable time on VM hardware
- [ ] Dijkstra worked example prepared and integrated into slides
- [ ] Slides for Parts 1 and 2 ready (distribute via Moodle)

---

## Open Development Tasks

- [ ] **AP5:** Write `assignments/ros-fundamentals.md` (activity sheet for Part 4)
- [ ] **AP5:** Prepare launch file wrappers and VM setup README in `scripts/`
- [ ] **Dijkstra example:** Insert the prepared worked example into Section 1.5 of this file
- [ ] **VM performance:** Verify Gazebo runs at acceptable speed on lab VM specs (→ `docs/semester-prep.md`)

---

*Lecturer reference only.*
