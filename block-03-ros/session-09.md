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

Path planning in ROS is split into two separate layers that operate on different time horizons and at different scales:

| Layer | Role | Algorithm examples | Horizon |
|---|---|---|---|
| **Global planner** | Finds an optimal path through the full known map | Dijkstra, A* | Entire map; computed once per goal |
| **Local planner** | Executes the path in real time, reacting to dynamic obstacles | DWA (Dynamic Window Approach) | Small window around robot; re-computed at ~10 Hz |

---

#### Global Planner — Dijkstra Algorithm

The global planner treats the occupancy grid map as a **graph**: each free cell is a node, and edges connect neighbouring cells with a cost that reflects how desirable it is to pass through that area (cells near obstacles are assigned higher costs via the *costmap*).

**Dijkstra's algorithm** guarantees the shortest path in a graph with non-negative edge weights. It works as follows:

1. Assign cost **0** to the start node; assign **∞** to all other nodes.
2. From all unvisited nodes, select the one with the lowest current cost.
3. For each neighbour of that node: if the path *through* the current node is shorter than the neighbour's current cost, update it.
4. Mark the current node as visited (it will not be revisited).
5. Repeat from step 2 until the goal node is visited.
6. Trace the shortest path backwards from goal to start.

**Worked example — warehouse routing:**

Consider a simplified warehouse with six locations. Edge weights represent travel distance in metres.

```
  S ──2── A ──5── C
  │       │       │
  4       1       2
  │       │       │
  B ──3── D ──1── G
```

Nodes: **S** (Start), **A**, **B**, **C**, **D**, **G** (Goal)

Edges: S→A: 2 · S→B: 4 · A→B: 1 · A→C: 5 · B→D: 3 · D→C: 1 · D→G: 6 · C→G: 2

**Step-by-step execution:**

| Step | Visited node | Cost at visit | Updated neighbours (new cost) | Unvisited set (node: cost) |
|---|---|---|---|---|
| Init | — | — | — | S:0, A:∞, B:∞, C:∞, D:∞, G:∞ |
| 1 | **S** | 0 | A: 0+2=**2**, B: 0+4=**4** | A:2, B:4, C:∞, D:∞, G:∞ |
| 2 | **A** | 2 | B: min(4, 2+1)=**3**, C: 2+5=**7** | B:3, C:7, D:∞, G:∞ |
| 3 | **B** | 3 | D: 3+3=**6** | C:7, D:6, G:∞ |
| 4 | **D** | 6 | C: min(7, 6+1)=**7**, G: 6+6=**12** | C:7, G:12 |
| 5 | **C** | 7 | G: min(12, 7+2)=**9** | G:9 |
| 6 | **G** | 9 | — | — |

**Result:** Shortest path cost = **9 m**

**Path trace (backwards):** G ← C ← A ← S → **S → A → C → G**

The naive-looking route S → B → D → C → G would cost 4+3+1+2 = 10 m — Dijkstra correctly found the shorter alternative despite an initial detour through A.

**Key takeaway for students:** Dijkstra always finds the globally optimal path, but it explores the entire map (or large parts of it) to do so. For small maps this is fine; for large grids it can be slow.

---

#### Global Planner — A* as an Improvement

A* is a common alternative that uses a **heuristic** (typically the straight-line distance to the goal) to guide the search preferentially towards the goal. This reduces the number of nodes explored and speeds up planning considerably, while still guaranteeing the optimal path (provided the heuristic never overestimates the true cost).

**Comparison:**

| Property | Dijkstra | A* |
|---|---|---|
| Optimality | Always optimal | Optimal with admissible heuristic |
| Search direction | Uniform (expands in all directions) | Guided towards goal |
| Speed | Slower on large maps | Much faster in practice |
| ROS default | Used as fallback | Default in many ROS configurations |

**Teaching note:** The key intuition is that A* "knows roughly which direction the goal is" while Dijkstra "has no idea and checks everywhere equally."

---

#### Local Planner — Dynamic Window Approach (DWA)

Once the global planner has produced a path, the **local planner** is responsible for actually driving the robot along it. The local planner re-plans every 100 ms or so, using only the most recent sensor data within a small window around the robot.

**Why not just follow the global path exactly?**
The global map may be outdated — a person or forklift may have moved into the robot's path. The local planner handles these dynamic obstacles in real time.

**DWA works as follows:**

1. **Sample feasible velocities:** Generate a set of candidate velocity pairs (linear velocity *v*, angular velocity *ω*) that the robot can physically reach within one time step given its current speed and acceleration limits. This is the *dynamic window*.
2. **Simulate trajectories:** For each candidate velocity, simulate the robot's trajectory over a short horizon (e.g. 2–3 seconds).
3. **Score each trajectory** using a cost function that penalises:
   - Distance to obstacles (safety)
   - Deviation from the global path (staying on route)
   - Distance to the goal heading (progress)
4. **Select the best trajectory** (lowest cost) and send its velocity command to the drive controller.

**Teaching note:** Show the DWA visualisation in RViz (the fan of candidate trajectories in different colours). Students find this intuitive — the robot "tries out" possible futures and picks the best one.

---

#### Costmaps

Both planning layers use a **costmap** — a grid that annotates each cell of the map with a traversal cost:

| Cell type | Cost | Meaning |
|---|---|---|
| Free space, far from obstacles | 0 | Robot can pass without penalty |
| Inflated zone (near obstacle) | 1–252 | Path planner steers away to maintain clearance |
| Inscribed zone (inside robot footprint if centred here) | 253 | Robot body would touch obstacle — avoid |
| Lethal obstacle | 254 | Collision — strictly forbidden |

The *inflation radius* is a configurable parameter: a larger value produces more conservative, obstacle-shy paths; a smaller value allows the robot to pass closer to obstacles.

**Two separate costmaps in ROS:**
- **Global costmap** — built once from the static map; used by the global planner.
- **Local costmap** — updated continuously from live sensor data; used by the local planner for real-time obstacle avoidance.

---

**Connection to practice:** In ROS, the `move_base` node orchestrates both planners. When a goal pose is sent (via RViz or programmatically), `move_base` calls the global planner to compute a path, then hands execution over to the local planner, which continuously adjusts velocity commands until the goal is reached or the path is blocked.

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
- [ ] **VM performance:** Verify Gazebo runs at acceptable speed on lab VM specs (→ `docs/semester-prep.md`)

---

*Lecturer reference only.*
