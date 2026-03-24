# Block 3 — Autonomous AGVs with ROS

Introduction to autonomous AGV technology and ROS (Robot Operating System) as the standard middleware for autonomous robots. Given the non-programmer target group, this block is structured around lecturer/hardware demos and guided student activities using pre-written scripts.

## Rationale

Modern autonomous AGVs rely on sensor fusion, localisation, and path planning — and ROS is the de-facto middleware that ties all these components together. Exposure to both layers gives students literacy in the vocabulary and architecture of real-world autonomous systems, even without becoming proficient programmers.

## Approach for Non-Programmers

- Lecturer and hardware demos take centre stage; students observe, ask questions, and analyse.
- Student activities consist of **running pre-written, pre-configured scripts** and interpreting the output.
- The focus shifts from *building* to *understanding*: what does this component do, why does it work this way, what would change if…?
- The complete TurtleBot3 workflow (simulation → real hardware) serves as a unifying red thread across both sessions.

*Assumption:* Pre-configured VMs with a working ROS + Gazebo environment will be provided. Setting up ROS from scratch is not a student task. VM performance with Gazebo must be verified — not yet confirmed.

---

## Unit 3.1 — Autonomous AGV Technology & ROS Fundamentals

### Content: Autonomous AGV Technology (lecturer presentation)

A conceptual introduction to the technical layers that make autonomous navigation possible. Embedded here as context for understanding what ROS manages.

| Concept | Description |
|---|---|
| **Sensors** | Laser scanner (LiDAR), camera, IMU, ultrasonic — what each measures and what it is good for |
| **Dead reckoning (Koppelnavigation)** | Position estimate from wheel odometry; why it drifts over time |
| **Landmark-based localisation (Peilen)** | Natural landmarks, reflector targets, AprilTags — how the robot corrects its position estimate |
| **Probabilistic localisation** | Particle filter (AMCL), EKF — intuition without maths |
| **Path planning** | Global planner (A\*, Dijkstra) vs. local planner (DWA) — difference and interplay |
| **SLAM** | Simultaneous Localisation and Mapping — why it is needed and what it produces |

### Content: ROS Basics (lecturer presentation)

- Why ROS? Motivation, history, and industry relevance
- Advantages of ROS: modularity, large community, hardware abstraction, reusability across platforms
- ROS architecture: nodes, topics, messages, services, actions — conceptual overview
- Packages and workspaces
- Key packages and tools:

| Package / Tool | Role |
|---|---|
| **Gazebo** | Physics-based robot simulator |
| **RViz** | Visualisation of sensor data, maps, and robot state |
| **Navigation Stack** | Combines AMCL, move\_base, costmaps for autonomous navigation |
| **gmapping / Cartographer** | SLAM implementations |
| **teleop\_twist\_keyboard** | Keyboard-based manual driving |

- **Live demo:** TurtleBot3 sensor data (LiDAR, odometry) streamed as ROS topics; students observe in RViz in real time

### Guided Student Activity

- Open the pre-configured ROS environment on the VM (TurtleBot3 simulation in Gazebo)
- Run provided launch scripts to start the simulated robot
- Use `rostopic echo` and `rqt_graph` to inspect data flow — command execution only, no coding
- Identify: which node publishes sensor data, which node subscribes, what message type is used

**Deliverable:** Students can describe the node-topic architecture and identify what data is flowing in a given ROS system.

**To do:** Write a guided activity sheet (→ AP5)

---

## Unit 3.2 — SLAM, Navigation, and the TurtleBot3 Workflow

### Content: SLAM and Navigation (lecturer presentation, embedded into workflow)

Rather than treating SLAM and path planning as abstract topics, they are introduced through the concrete TurtleBot3 workflow — theory and practice are interleaved.

**Workflow steps introduced:**

1. **Bring up the robot** — launch file starts all hardware/simulation drivers and sensors
2. **Teleoperation** — manually drive the robot using keyboard input; introduces odometry and velocity topics
3. **SLAM mapping** — drive manually to build a map; observe gmapping constructing the occupancy grid in RViz
4. **Save the map** — export the finished map as a file used by the navigation stack
5. **Autonomous navigation** — load the saved map, launch AMCL for localisation, set a 2D navigation goal in RViz; observe the global path and local obstacle avoidance

### Guided Student Activity

- Launch a pre-configured SLAM session in **Gazebo** (TurtleBot3 world provided)
- Step through the workflow above using provided launch files and scripts
- Observe the map being built in RViz; then send a navigation goal and watch autonomous driving

### Lecturer Demo — Real TurtleBot3

- Repeat the same workflow on the physical TurtleBot3 in the lab
- Students observe the difference between simulation and real-hardware behaviour (sensor noise, map quality)
- Discussion: what assumptions did the simulation make that reality violates?

**Deliverable:** Students can explain each step of the TurtleBot3 workflow and describe what SLAM achieves and one limitation of the approach.

**To do:** Write a guided activity sheet with pre-configured launch files (→ AP6)

---

## Unit 3.3 — Manipulation (Lecturer Demo Only)

*This unit is a brief lecturer demonstration — there is no student activity.*

### Content (lecturer demo)

- Introduction to robot arm control via ROS and MoveIt
- **Live demo:** LoCoBot arm with gripper performing a pick-and-place sequence
- Discussion: how does manipulation extend the intralogistics use case (goods-to-person, depalletising)?

**Note:** This demo is time-permitting. If sessions run long, it can be dropped without affecting student deliverables.

---

## Hardware Demos (Lecturer)

| Unit | Hardware | Demo content |
|---|---|---|
| 3.1 ROS Fundamentals | TurtleBot3 | Sensor data (LiDAR, odometry) streamed as live ROS topics |
| 3.2 SLAM & Navigation | TurtleBot3 | Live SLAM mapping and autonomous navigation |
| 3.3 Manipulation | LoCoBot (arm + gripper) | Pick-and-place sequence (time-permitting) |

---

## Folder Structure

| Folder | Contents |
|---|---|
| `assignments/` | Guided activity sheets for students |
| `scripts/` | Pre-written ROS scripts and launch files; students run these |

## Activity Status

| Unit | Activity Sheet | Scripts | Status |
|---|---|---|---|
| 3.1 ROS Fundamentals | `assignments/ros-fundamentals.md` | `scripts/` | ⏳ To do (AP5) |
| 3.2 SLAM & Navigation | `assignments/slam-navigation.md` | `scripts/` | ⏳ To do (AP6) |
| 3.3 Manipulation | — (demo only) | `scripts/locobot_motion.py` | ⏳ Demo script to prepare (AP7 revised) |
