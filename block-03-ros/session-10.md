# Session 10 — SLAM, Navigation & TurtleBot3 Workflow

> **Duration:** 3 h · **Graded:** No

**Goal:** Students execute the complete TurtleBot3 autonomous navigation workflow step by step in the Gazebo simulation and document what they observe. They can explain the role of SLAM, localisation, and path planning in a running system — connecting theory from Session 9 to observable behaviour.

---

## Agenda Overview

| Time | Phase | Format |
|---|---|---|
| 0:00 – 0:20 | Part 1: Recap & Workflow Introduction | Lecturer presentation |
| 0:20 – 1:50 | Part 2: Guided Student Activity — TurtleBot3 Workflow in Gazebo | Individual / pair work |
| 1:50 – 2:20 | Part 3: Live Demo — Real TurtleBot3 | Lecturer hardware demo |
| 2:20 – 3:00 | Part 4: Discussion & Written Deliverable | Plenary + individual work |

---

## Part 1 — Recap & Workflow Introduction (20 min)

### Recap (5 min)

Brief review of Session 9 concepts students need for today:
- Odometry drifts → SLAM corrects by matching LiDAR scans to a growing map
- Particle filter (AMCL) narrows down where the robot is on a *known* map
- Path planner uses the map to find a route to the goal

**Key distinction for today:**
- **Mapping phase** (SLAM with `gmapping`): the map does not exist yet; robot builds it while exploring
- **Navigation phase** (AMCL + `move_base`): the map exists; robot localises itself and plans a path

### The TurtleBot3 Workflow (15 min)

Introduce the five steps students will execute. Show the overall flow diagram:

```
[Bring-up]
    │
    ▼
[Teleoperation]  ──►  [SLAM Mapping]  ──►  [Save Map]
                                                │
                                                ▼
                                       [Autonomous Navigation]
                                       (AMCL + move_base)
```

Explain: Steps 1–4 are always done in sequence. Step 5 requires the saved map from Step 4.

---

## Part 2 — Guided Student Activity: TurtleBot3 Workflow in Gazebo (90 min)

**Setup:** Pre-configured VMs. All launch files and a step-by-step activity sheet are provided.

**Activity sheet:** `assignments/slam-navigation.md` (→ AP6)

---

### Step 1 — Bring-Up (5 min)

Launch the TurtleBot3 simulation in Gazebo. This starts all required nodes: the robot model, simulated sensors (LiDAR, odometry), and the ROS parameter server.

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

**Students observe in Gazebo:** The robot appears in a pre-built world. LiDAR rays are visible. In RViz (second terminal), the `/scan` topic shows the laser data.

**Reflection question:** Which nodes are now running? Run `rosnode list` and note the answer.

---

### Step 2 — Teleoperation (10 min)

Drive the robot manually using keyboard input. This sends velocity commands on `/cmd_vel`.

```bash
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```

**Students observe:** The robot moves in Gazebo in response to key presses. In a second terminal, `rostopic echo /odom` shows the odometry updating.

**Reflection question:** Drive the robot in a square. Does it end up exactly where it started? Why or why not?

---

### Step 3 — SLAM Mapping (35 min)

Launch `gmapping`. The SLAM node subscribes to `/scan` and `/odom` and begins building an occupancy grid map.

```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```

Open RViz (pre-configured profile provided). Students will see:
- The occupancy grid map growing as they drive
- Grey cells = unknown, white = free, black = occupied (obstacle)
- The particle cloud (AMCL disabled during mapping — this is pure SLAM)

Students drive through the entire world slowly, covering all corridors. The map should be complete (no large grey areas) before proceeding.

**Reflection question:** What happens to the map quality if you drive too fast? Note your observations.

---

### Step 4 — Save the Map (5 min)

Export the finished map to two files: a `.pgm` image (the grid) and a `.yaml` metadata file (resolution, origin).

```bash
rosrun map_server map_saver -f ~/map
```

**Students observe:** Two files appear in the home directory. Open `map.pgm` in an image viewer — it shows the same map as RViz.

**Reflection question:** What information is stored in `map.yaml`? Open and read the file.

---

### Step 5 — Autonomous Navigation (35 min)

Shut down the SLAM launch file. Now load the saved map and launch the navigation stack. This starts AMCL (localisation) and `move_base` (path planning + execution).

```bash
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
```

**Initial pose estimate:**
1. In RViz, use the "2D Pose Estimate" button to tell the robot approximately where it is on the map.
2. The particle cloud appears — it is initially spread out (high uncertainty).
3. Drive the robot a little with `teleop_twist_keyboard` to help AMCL converge → the cloud narrows.

**Send a navigation goal:**
1. In RViz, use the "2D Nav Goal" button and click a target position on the map.
2. The global planner draws the intended path (green line).
3. The robot drives autonomously, avoiding obstacles with the local planner (DWA).

**Students observe:**
- The planned path updating as the robot moves
- The particle cloud shifting as localisation refines
- The robot stopping if an obstacle blocks the path and replanning

**Reflection questions:**
1. How does the path change if you place a virtual obstacle in front of the robot?
2. What is the role of AMCL once the map is loaded? How does it differ from gmapping?
3. Where in this workflow does the Dijkstra/A* algorithm run?

---

## Part 3 — Live Demo: Real TurtleBot3 (30 min)

**Hardware:** Real TurtleBot3, connected to lecturer laptop.

**Demo:** Repeat the same five-step workflow on the physical robot in the room.

| Simulation | Reality | Discussion point |
|---|---|---|
| Gazebo world is perfectly clean | Real environment has lighting changes, reflective surfaces, dynamic objects | Map quality differs |
| Odometry is noise-free | Wheel slip on carpet; IMU drift | AMCL needs to work harder |
| LiDAR returns are perfect | Glass walls invisible; thin legs may be missed | Safety implications for industrial AGVs |
| Navigation always succeeds if map is correct | Robot may get stuck; recovery behaviours activate | Robustness in real deployments |

**Discussion prompt:** *"You have seen the same workflow in simulation and on real hardware. Where would you invest engineering effort to make a real AGV deployment reliable?"*

---

## Part 4 — Discussion & Written Deliverable (40 min)

### Plenary Discussion (15 min)

- What surprised you compared to what you expected?
- In which intralogistics scenarios is SLAM most useful? When is a fixed map sufficient?
- What is the biggest limitation of this approach for a real warehouse?

### Written Deliverable (25 min, individual)

Students write a short structured report answering the following questions. Template provided in the activity sheet.

| Question | Expected answer depth |
|---|---|
| Describe the five steps of the TurtleBot3 workflow. What happens in each step? | 3–5 sentences per step |
| Explain in your own words: what does SLAM achieve, and why is it needed? | 1 paragraph |
| What is the difference between the mapping phase and the navigation phase? | 1 paragraph |
| Name two observations from the simulation that connect to a concept from Session 9. | 2–4 sentences each |
| (Optional) Name one limitation of the demonstrated approach for real industrial use and suggest how it could be addressed. | 1 paragraph |

**Submission:** End of session or next session at the latest (to be confirmed).

**Deliverable:** Written observation report. *(Graded — part of the 70% in-semester component)*

---

## Files

| File | Description | Status |
|---|---|---|
| `assignments/slam-navigation.md` | Step-by-step activity sheet + report template | ⏳ To do (AP6) |
| `scripts/` | Pre-configured RViz profile, map files for fallback | ⏳ To do (AP6) |

---

## Preparation Checklist (Lecturer)

- [ ] TurtleBot3 (real) charged; full workflow tested end-to-end in the lab room
- [ ] A pre-built map of the demo room is saved as fallback (in case live mapping runs overtime)
- [ ] Student VMs: `turtlebot3_gazebo`, `turtlebot3_slam`, `turtlebot3_navigation` packages installed and tested
- [ ] Pre-configured RViz launch file provided in `scripts/` (no manual panel setup needed)
- [ ] Report template included in activity sheet; submission process communicated
- [ ] Timing check: SLAM mapping in simulation takes approx. 30–35 min — do not underestimate

---

## Open Development Tasks

- [ ] **AP6:** Write `assignments/slam-navigation.md` (step-by-step activity sheet + report template)
- [ ] **AP6:** Prepare pre-configured RViz launch profile and add to `scripts/`
- [ ] **AP6:** Decide and document submission process for the written deliverable
- [ ] **Q4a:** Confirm weighting of this deliverable within the 70% in-semester grade

---

*Lecturer reference only.*
