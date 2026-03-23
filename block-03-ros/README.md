# Block 3 — Autonomous AGVs with ROS

Introduction to ROS (Robot Operating System) as the standard middleware for autonomous robots. Given the non-programmer target group, this block is structured around lecturer/hardware demos and guided student activities using pre-written scripts.

## Rationale

ROS is the de-facto standard middleware for autonomous robotics and is ubiquitous in industry. Exposure to ROS gives students literacy in the vocabulary and architecture of modern autonomous systems — even without becoming proficient programmers.

## Approach for Non-Programmers

The previous concept assumed Python knowledge and included student-led coding tasks (publishing topics, writing a ROS node from scratch). These are not feasible for this target group.

**Revised structure:**
- Lecturer and hardware demos take centre stage; students observe, ask questions, and analyse.
- Student activities consist of **running pre-written, pre-configured scripts** and interpreting the output.
- The focus shifts from *building* to *understanding*: what does ROS do here, why does it work this way, what would change if…?
- AP7 revised: students **modify a provided ROS node** (change parameters, add a simple behaviour step) rather than writing one from scratch.

*Assumption:* Pre-configured VMs with a working ROS environment will be provided. Setting up ROS from scratch is not a student task. VM performance with Gazebo must be verified — not yet confirmed.

---

## Unit 3.1 — ROS Fundamentals

### Content (lecturer presentation + demo)
- Why ROS? Motivation, history, and industry relevance
- ROS architecture: nodes, topics, messages, services — conceptual overview
- Packages and workspaces
- **Live demo:** Turtlebot3 sensor data streamed as ROS topics; students observe in real time

### Guided Student Activity
- Open a pre-configured ROS environment on the VM
- Run provided scripts to start and inspect a simulated robot (iRobot Create 3 simulator)
- Use `rostopic echo` and `rqt_graph` to visualise data flow — no coding, command execution only

**Deliverable:** Students can describe the node-topic architecture and identify what data is flowing in a given ROS system.

**To do:** Write a guided activity sheet (→ AP5)

---

## Unit 3.2 — SLAM and Navigation

### Content (lecturer presentation)
- Localisation approaches: GPS, AprilTags, indoor localisation
- SLAM (Simultaneous Localisation and Mapping): what it does and why it matters
- Path planning: global vs. local planners

### Guided Student Activity
- Launch a pre-configured SLAM session in the **Gazebo** simulator (Turtlebot3 environment provided)
- Drive the robot manually to build a map; observe the map being constructed in RViz
- Then send a navigation goal and observe autonomous path planning in action

### Lecturer Demo
- SLAM and autonomous navigation with the real **Turtlebot3**

**Planned future addition:** AprilTag localisation demo — not yet implemented

**Deliverable:** Students can explain what SLAM is doing in the demo and describe one limitation of the approach.

**To do:** Write a guided activity sheet with pre-configured launch files (→ AP6)

---

## Unit 3.3 — Manipulation

### Content (lecturer demo)
- Introduction to robot arm control via ROS and MoveIt
- **Live demo:** LoCoBot arm with gripper performing a pick-and-place sequence

### Guided Student Activity
- Open a provided LoCoBot simulation with a pre-written motion script
- Modify clearly marked parameters (target position coordinates, gripper timing) and observe the effect
- This is the AP7 activity: guided modification of an existing ROS node

**Deliverable:** Students document what they changed and how the robot's behaviour differed.

**To do:** Prepare the LoCoBot simulation environment and the parameterised motion script (→ AP7)

---

## Hardware Demos (Lecturer)

| Unit | Hardware | Demo content |
|---|---|---|
| ROS Fundamentals | Turtlebot3 | Sensor data streamed as live ROS topics |
| SLAM & Navigation | Turtlebot3 | Live SLAM and autonomous navigation |
| Manipulation | LoCoBot (arm + gripper) | Pick-and-place sequence |

---

## Folder Structure

| Folder | Contents |
|---|---|
| `assignments/` | Guided activity sheets for students |
| `scripts/` | Pre-written ROS scripts and launch files; students run and modify these |

## Activities

| Unit | Activity Sheet | Scripts | Status |
|---|---|---|---|
| ROS Fundamentals | `assignments/ros-fundamentals.md` | `scripts/` | ⏳ To do (AP5) |
| SLAM & Navigation | `assignments/slam-navigation.md` | `scripts/` | ⏳ To do (AP6) |
| Manipulation (LoCoBot) | `assignments/manipulation.md` | `scripts/locobot_motion.py` | ⏳ To do (AP7) |
