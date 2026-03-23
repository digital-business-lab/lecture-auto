# Course Concept: Autonomous Logistics Systems and IoT

> **Status:** Working draft — revised 2026-03-23
> This document is the authoritative description of the course structure, content, and pedagogy.
> It supersedes the informal notes from the previous semester.

---

## 1. Course Overview

| Field | Detail |
|---|---|
| **Title** | Autonomous Logistics Systems and IoT |
| **Level** | Master |
| **Topic focus** | Automated Guided Vehicles (AGVs) in intralogistics |
| **Format** | Lecture + hands-on labs (simulation and real hardware) |
| **Duration** | Approx. 13 sessions across one semester |

---

## 2. Target Group and Prerequisites

**Target group:** Master's students in business informatics, industrial engineering, or related fields.

**Assumed prerequisites:**
- Basic programming knowledge (Python preferred) — *assumed, not formally verified*
- General understanding of logistics and supply chain concepts
- No prior robotics or simulation experience required

**Open question:** Should prerequisites be formally communicated and checked before the course begins?

---

## 3. Learning Objectives

By the end of the course, students will be able to:

1. Explain the history, types, and technical components of AGVs and their role in modern intralogistics.
2. Model and program a simulated AGV in Webots to perform navigation tasks (obstacle avoidance, maze solving, line following).
3. Describe the architecture of ROS and implement basic robotics workflows (topics, nodes, navigation, SLAM).
4. Simulate and compare classical vs. AGV-supported manufacturing processes and evaluate the results.
5. Develop a structured business case for AGV deployment, including market research, cost-benefit analysis, and a requirements specification.

---

## 4. Course Structure Overview

| Block | Topic | Sessions | Approx. Duration |
|---|---|---|---|
| 1 | Organisation & Foundations | 1–2 | 2 weeks |
| 2 | Classical AGVs with Webots | 3–8 | 6 weeks |
| — | Field trip | — | 1 day |
| 3 | Autonomous AGVs with ROS | 9–10 | 2 weeks |
| 4 | AGV Simulation | 11–13 | 3 weeks |
| + | Additional assessment: Business Case | parallel | ongoing |

---

## 5. Block 1 — Organisation & Foundations

### Sessions 1–2

### Content

**Session 1 — Organisation**
- Course structure and schedule overview
- Topic assignment for student research (industry-specific AGV applications)

**Sessions 1–2 — AGV Fundamentals (lecturer presentation)**
- History and evolution of AGVs
- Modern application domains (automotive, e-commerce, healthcare, etc.)
- AGV technology deep-dive:
  - Navigation and guidance systems (inductive, laser, natural navigation)
  - Safety systems and standards
  - Fleet management and control systems
  - Vehicle types and load handling
  - Operating environment requirements
  - Future trends (AI-based navigation, collaborative robots)

**Student research component**
- Students research and present industry-specific AGV applications
- *Rationale:* Keeps lecturer content focused on technical foundations; builds student ownership

### Pedagogy
- Lecturer input for technical foundations
- Student presentations for industry context
- *Decision (2026-03-23):* Terminology definition section removed — learning benefit too low relative to time cost

### Deliverables
- Students: short research presentation on industry-specific AGV applications

---

## 6. Block 2 — Classical AGVs with Webots

### Sessions 3–8 (approx. 6 weeks)

### Rationale
Webots provides a free, cross-platform robot simulator that is well-suited for teaching AGV fundamentals without requiring immediate hardware access. Students build practical programming skills alongside conceptual understanding.

*Assumption:* Students have no prior Webots experience. All Webots-specific knowledge must be introduced in the course material.

### Known issue from last semester
Students struggled significantly with Webots onboarding; the labyrinth assignment required a time extension. Root cause is assumed to be tool unfamiliarity, not algorithm complexity — *this assumption is not yet validated*.

### Planned improvements
- Provide structured introductory tutorial before first assignment (→ AP2)
- Provide the labyrinth world pre-built so students focus on AGV behaviour (→ AP3)
- Clarify or simplify the VM setup process

---

### Assignment 1 — Obstacle Avoidance

**Goal:** Students get hands-on with Webots and implement their first AGV controller.

**Tasks:**
1. Set up the Webots environment (VM or local installation)
2. Model a custom robot (basic geometry and sensor configuration)
3. Implement a controller that navigates an environment while avoiding obstacles

**Pedagogy:** Fully hands-on; instructor available for support. Students work in the VM environment provided.

**Deliverable:** Working Webots simulation demonstrating obstacle avoidance behaviour.

**Hardware extension:** — (none for this assignment)

---

### Assignment 2 — Labyrinth

**Goal:** Students implement a maze-solving algorithm and transfer it to physical hardware.

**Tasks:**
1. Receive a pre-built labyrinth world in Webots *(improvement from last semester)*
2. Develop and refine a maze-solving algorithm within the simulation
3. Present results and explain algorithmic approach

**Pedagogy:** Independent work phase (approx. 2 sessions) followed by group presentations.

**Deliverable:** Presentation of labyrinth solution; working simulation demo.

**Hardware extension:** Lecturer demonstrates the algorithm on the **Alphabot** (physical hardware demo).

**Open question:** Should students also run their own algorithm on the Alphabot, or is the lecturer demo sufficient?

---

### Assignment 3 — Line Following

**Goal:** Students implement line-tracking behaviour at two complexity levels.

**Tasks:**

*Basic (all students):*
1. Implement line following in Webots with 4 sensors on a standard track

*Extended (optional or advanced):*
2. Adapt the controller for 8 sensors and tracks with varying colours

**Pedagogy:** Assignment handout → independent work session → presentation of results. A competition-style evaluation is considered (*not yet decided*).

**Deliverable:** Working line-following simulation; presentation of approach and results.

**Hardware extension:** Lecturer demonstrates line following on the **Dobot** robot.

**To do before delivery:**
- Define and write the line-following tutorial for Webots (→ AP4)
- Assemble and test the Dobot hardware
- Consider embedding a video of a previous line-following competition

---

### Field Trip

Embedded within Block 2. Students visit an industrial site with AGV deployment in operation.

*Assumption:* Field trip location and date will be coordinated separately; not yet confirmed for the new semester.

---

## 7. Block 3 — Autonomous AGVs with ROS

### Sessions 9–10 (approx. 2 weeks)

### Rationale
ROS (Robot Operating System) is the de-facto standard middleware for autonomous robotics. Introducing it at this stage builds on the simulation skills from Block 2 and prepares students for industry-relevant tooling.

*Assumption:* Students have basic Python knowledge going into this block. No prior ROS experience expected.

### Known issue from last semester
The ROS block is outlined but hands-on assignments are not yet fully developed. The current structure may not provide enough depth for meaningful skill development in only two sessions.

---

### Unit 3.1 — ROS Fundamentals

**Content (lecturer presentation + demo):**
- Why ROS? Motivation and industry relevance
- ROS architecture: nodes, topics, messages, services
- Packages and workspaces
- Live demo: reading sensor data from a Turtlebot via ROS topics

**Hands-on (students):**
- Set up the ROS environment
- First experiments using the **iRobot Create 3 simulator**
- Publish and subscribe to basic topics

**Deliverable:** Students can run a basic ROS setup and interact with topics.

**To do:** Write a detailed assignment sheet for this unit (→ AP5)

---

### Unit 3.2 — SLAM and Navigation

**Content (lecturer presentation):**
- Localisation approaches: GPS, AprilTags, indoor localisation
- SLAM (Simultaneous Localisation and Mapping): principles and algorithms
- Path planning: global vs. local planners

**Hands-on (students):**
- SLAM and autonomous navigation in the **Gazebo** simulator (Turtlebot 3 or 4)

**Lecturer demo:**
- SLAM and navigation with a real **Turtlebot 3 or 4**

**Planned future addition:** AprilTag demo (tags for localisation on the Turtlebot) — *not yet implemented*

**Deliverable:** Students successfully map an environment and navigate autonomously in Gazebo.

**To do:** Write a detailed assignment sheet for this unit (→ AP6)

---

### Unit 3.3 — Manipulation

**Content (lecturer demo):**
- Introduction to robot arm control via ROS
- Demo: **LoCoBot** robot arm in motion

**Hands-on (students):**
- Program a Python-based motion sequence for the LoCoBot using its simulator

**Planned future addition:** Mini-project — students design and implement a custom ROS node from scratch (→ AP7)

---

## 8. Block 4 — AGV Simulation

### Sessions 11–13 (approx. 3 weeks)

### Rationale
Students apply their accumulated knowledge by simulating a complete manufacturing scenario. The contrast between a classical production layout and one supported by AGVs motivates a data-driven evaluation of AGV impact.

### Scenario
**Wave manufacturing** — students simulate a production environment in two configurations:
1. Classical layout (no AGVs)
2. AGV-supported layout

They analyse throughput, lead times, and bottlenecks, and draw conclusions about the value of AGV deployment.

### Known issue
The task has no concrete problem statement, requirements, or evaluation criteria yet. Students and lecturer need a structured assignment (→ AP8).

### Open questions
- Which simulation tool should students use?
  - **Webots** (already familiar from Block 2) — low additional overhead, but not a logistics simulator
  - **Python-based custom simulation** — flexible, but requires significant scaffolding
  - **Dedicated logistics simulation tool** (e.g. AnyLogic, Plant Simulation, FlexSim) — industry-standard, but steep learning curve and potential licensing cost
- Should this be an individual or group assignment?
- Should results be presented, submitted as a report, or both?

*Preferred approach not yet decided — needs discussion before next semester.*

---

## 9. Additional Assessment — Business Case

### Rationale
A business case exercise connects the technical content to real-world decision-making. Students learn to justify AGV investments with quantitative and qualitative arguments.

### Components

| Component | Description |
|---|---|
| Market research | Survey of available AGV systems, vendors, and current market trends |
| Business case calculation | ROI, payback period, cost-benefit analysis for a defined scenario |
| Requirements specification (Lastenheft) | Structured requirements document for an AGV procurement |
| Utility value analysis (Nutzwertanalyse) | Weighted scoring of AGV alternatives against defined criteria |

### Known issue
No template, rubric, or clear scope exists yet. It is also unclear whether this is a mandatory or optional assessment (→ AP9).

### Open questions
- Mandatory or optional?
- Individual or group work?
- Integrated into Block 4, or run in parallel throughout the semester?
- Is there a real or fictional company scenario, or do students define their own?

---

## 10. Tools and Infrastructure

| Tool | Purpose | Availability |
|---|---|---|
| **Webots** | AGV simulation (Blocks 2, potentially 4) | Free, open-source; VM provided |
| **Alphabot** | Physical hardware demo (labyrinth) | Available in lab |
| **Dobot** | Physical hardware demo (line following) | Needs assembly and testing |
| **ROS** | Autonomous robotics middleware (Block 3) | Free, open-source; environment setup required |
| **Gazebo** | ROS-integrated simulator (SLAM/navigation) | Free, open-source |
| **Create 3 Simulator** | First ROS experiments | Free |
| **LoCoBot** | Manipulation demo + simulation | Available in lab |
| **Turtlebot 3/4** | SLAM & navigation (real hardware demo) | Available in lab |

*Assumption:* All listed hardware is operational and available for the new semester. This has not been verified for each item.

---

## 11. Open Questions and Next Steps

| # | Question | Priority |
|---|---|---|
| Q1 | Which tool will be used for Block 4 AGV simulation? | High |
| Q2 | Is the Business Case a mandatory or optional assessment? | High |
| Q3 | How is the Business Case integrated into the course schedule? | Medium |
| Q4 | Should students also run their own algorithm on the Alphabot (labyrinth)? | Medium |
| Q5 | Are all hardware items tested and ready for the new semester? | Medium |
| Q6 | Should prerequisites be formally verified before the course begins? | Low |
| Q7 | Is a line-following competition format used, and how is it evaluated? | Low |

---

*Document created 2026-03-23. Maintained alongside `CLAUDE.md`.*
