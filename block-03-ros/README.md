# Block 3 — Autonomous AGVs with ROS

Two interleaved themes: (1) the technical building blocks of autonomous navigation (sensors, localisation, path planning, SLAM) and (2) ROS as the middleware that ties these components together. The TurtleBot3 serves as a unifying example throughout — first in simulation (Gazebo), then as a live hardware demo.

Given the non-programmer target group, student activities consist entirely of running pre-written scripts and interpreting the output. Students observe and analyse — they do not write ROS code.

## Contents

| Item | Description |
|---|---|
| `session-09.md` | Detailed lecturer reference: Session 9 agenda, preparation checklist |
| `session-10.md` | Detailed lecturer reference: Session 10 agenda, preparation checklist |
| `assignments/` | Guided activity sheets handed out to students |
| `scripts/` | Pre-written ROS launch files and scripts; students run these |
| Lecture slides | Distributed via Moodle (contain third-party images) |

---

## Session 9 — AGV Technology & ROS Fundamentals (3 h)

### Content
- Autonomous AGV technology: sensors, dead reckoning, landmark localisation, probabilistic localisation, path planning (Dijkstra), SLAM
- ROS architecture: nodes, topics, messages, key packages (Gazebo, RViz, Navigation Stack)
- Live demo: TurtleBot3 sensor data streamed as ROS topics in RViz

### Deliverables
- None (ungraded introduction)

→ See [`session-09.md`](session-09.md) for full details.

---

## Session 10 — SLAM, Navigation & TurtleBot3 Workflow (3 h)

### Content
- The complete TurtleBot3 workflow: bring-up → teleoperation → SLAM mapping → save map → autonomous navigation
- Students run through each step in the Gazebo simulation using provided launch files
- Live hardware demo: same workflow on the real TurtleBot3
- Plenary discussion: simulation vs. reality, intralogistics implications

### Deliverables
- None (ungraded)

→ See [`session-10.md`](session-10.md) for full details.

---

## Hardware Demos (Lecturer)

| Session | Hardware | Demo content |
|---|---|---|
| 9 | TurtleBot3 | Sensor data (LiDAR, odometry) as live ROS topics in RViz |
| 10 | TurtleBot3 | Full SLAM and autonomous navigation run on real hardware |
| 10 (optional) | LoCoBot (arm + gripper) | Pick-and-place via ROS/MoveIt — time-permitting only |

---

## Pedagogy

- No from-scratch coding: students run provided launch files and scripts, modify parameters at most
- Pre-configured VMs with ROS and Gazebo are required — students do not set up the environment
- The TurtleBot3 workflow serves as a concrete red thread linking all theoretical concepts to observable behaviour
- VM performance with Gazebo must be verified before the semester (→ `docs/semester-prep.md`)
