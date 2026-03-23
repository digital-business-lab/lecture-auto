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
| **Assessment** | Two components: 70% in-semester (Webots, ROS, simulation) + 30% semester break (business case) |

---

## 2. Target Group and Prerequisites

**Target group:** Master's students in **business administration (BWL)**.

**Programming background:** None. Students have no prior experience with Python, C++, or any other programming language. This is a confirmed fact, not an assumption, and it is the single most important constraint shaping all hands-on activities in this course.

**Other assumed prerequisites:**
- General understanding of business processes and supply chain concepts (core BWL competency)
- Basic digital literacy (file management, browser, office tools)
- No prior robotics, simulation, or Linux experience expected

**Implication for course design:** All student-facing coding activities must use pre-written templates. Students fill in clearly marked logic gaps and modify parameters — they never write code from scratch. The primary learning goals in technical blocks are *understanding* and *evaluation*, not *implementation*.

---

## 3. Learning Objectives

By the end of the course, students will be able to:

1. Explain the history, types, and technical components of AGVs and their role in modern intralogistics.
2. Navigate and use a robotics simulation environment (Webots) to run and modify pre-defined AGV behaviours (obstacle avoidance, maze solving, line following).
3. Describe the architecture of ROS and understand how its core concepts (nodes, topics, messages) enable autonomous robot behaviour.
4. Interpret the results of a simulation comparing classical vs. AGV-supported manufacturing and draw business conclusions.
5. Develop a structured business case for AGV deployment, including market research, cost-benefit analysis, a requirements specification, and a utility value analysis.

**Note on objective 2:** Students modify and complete provided code templates; the learning goal is understanding the relationship between parameters/logic and observable robot behaviour — not programming proficiency.

---

## 4. Course Structure Overview

| Block | Topic | Sessions | Approx. Duration | Assessment weight |
|---|---|---|---|---|
| 1 | Organisation & Foundations | 1–2 | 2 weeks | — |
| 2 | Classical AGVs with Webots | 3–8 | 6 weeks | part of 70% |
| — | Field trip | — | 1 day | — |
| 3 | Autonomous AGVs with ROS | 9–10 | 2 weeks | part of 70% |
| 4 | AGV Simulation | 11–13 | 3 weeks | part of 70% |
| + | Business Case | semester break | — | 30% |

**Assessment structure:**
- **Assessment Component 1 (70%) — in-semester:** Hands-on assignments across Blocks 2, 3, and 4 (Webots tasks, ROS activities, Plant Simulation). Submitted and evaluated during the semester.
- **Assessment Component 2 (30%) — semester break:** Business case. Submitted after the semester ends.

*Open question:* How is the 70% distributed internally across Blocks 2, 3, and 4? Not yet decided.

---

## 5. Block 1 — Organisation & Foundations

### Sessions 1–2 (3 hours each)

### Content

**Session 1 — Organisation & AGV Foundations**
- Course structure, schedule, assessment overview, tools & infrastructure
- AGV epochs — four phases of development (group work + short presentations)
- Task-related aspects of AGV deployment (load types, flow regularity, throughput)
- Deployment modes (unit load carrier, towing, fork AGV, underride, assembly)
- Alternatives to AGVs (conveyors, forklifts, AMRs, manual transport)
- Suitability of alternatives — which solution fits which scenario? (group work + short presentations)

**Session 2 — AGV Technology**
- Industry-specific aspects and examples: automotive, e-commerce, healthcare, food, pharma (group work + plenary discussion)
- Technology of the overall system: navigation & guidance, fleet management, safety, WMS/ERP integration
- Technology of the transport vehicles: vehicle types, load handling, energy supply, sensor systems

### Pedagogy
- Alternates between short lecturer input and group work throughout both sessions
- Group work tasks are scenario- or sector-based; each group reports back in 2–3 min
- *Decision (2026-03-23):* Terminology definition section removed — learning benefit too low relative to time cost
- *Update (2026-03-23):* Sessions extended to 3 h each; group work and short presentations integrated directly into both sessions

### Deliverables
- Session 1: group presentations on AGV epochs and alternative suitability (in-session)
- Session 2: group report-back on industry-specific AGV applications (in-session)

---

## 6. Block 2 — Classical AGVs with Webots

### Sessions 3–8 (approx. 6 weeks)

### Rationale
Webots provides a free, cross-platform robot simulator suitable for teaching AGV fundamentals without requiring immediate hardware access. Hands-on work in simulation makes abstract concepts tangible and prepares students for the hardware demos.

### Coding approach: Template-based ("Light Coding")
Because students have no programming background, all Webots assignments use the following structure:
- A **complete, working controller** is provided as the starting point.
- Sections that encode the core logic (decision thresholds, sensor weights, state transitions) are replaced with **clearly marked `TODO` gaps**.
- Students read the surrounding code (with explanations) to understand *what* it does, then complete the gaps based on the assignment instructions.
- Students never write a controller from scratch.

This approach preserves the hands-on learning benefit while removing the barrier of syntax and language unfamiliarity. It also allows the lecturer to control the complexity precisely.

*Assumption:* Even with templates, some students will find Python syntax confusing. The templates must therefore include extensive inline comments explaining every non-trivial line. This has not been tested yet.

### VM Setup
All Webots work runs on virtual machines in the computer lab. A step-by-step setup guide will be provided (→ AP2). VM performance with Webots must be verified before the semester begins — *not yet confirmed*.

---

### Assignment 1 — Obstacle Avoidance

**Goal:** Students get hands-on with Webots and complete their first AGV controller.

**Tasks:**
1. Set up the Webots environment on the provided VM (guided by tutorial → AP2)
2. Open a pre-built world with a pre-modelled robot
3. Read through the provided controller template and understand the sensor-to-action logic
4. Complete the marked `TODO` sections (e.g. distance thresholds, turning direction logic)
5. Run and observe the simulation; adjust parameters and observe the effect

**Deliverable:** Working simulation demonstrating obstacle avoidance. Students document: which parameters they chose and why, what behaviour changed when they adjusted values.

**Hardware extension:** None for this assignment.

---

### Assignment 2 — Labyrinth

**Goal:** Students implement a maze-solving strategy by completing a provided template, then transfer the result to physical hardware (via lecturer demo).

**Tasks:**
1. Receive a **pre-built labyrinth world** in Webots *(improvement from last semester — students do not model the environment)*
2. Receive a controller template implementing the basic robot loop; complete the maze-solving logic gaps (e.g. wall-following decision rules)
3. Refine and test the algorithm within the simulation
4. Present approach and results to the group

**Pedagogy:** Independent work phase (approx. 2 sessions) followed by group presentations.

**Deliverable:** Presentation of maze-solving approach; working simulation demo.

**Hardware extension:** Lecturer demonstrates a maze-solving algorithm on the **Alphabot** (physical hardware demo). Students observe and compare real-world behaviour to simulation.

**Open question:** Should students also deploy their own algorithm on the Alphabot, or is the lecturer demo sufficient given the time and skill constraints?

---

### Assignment 3 — Line Following

**Goal:** Students implement line-tracking behaviour at two complexity levels using provided templates.

**Tasks:**

*Basic (all students):*
1. Complete a template controller for line following with 4 sensors on a standard track
2. Test and tune sensor weights and speed parameters

*Extended (optional or for advanced students):*
3. Adapt the controller for 8 sensors and tracks with varying colours (additional `TODO` sections in an extended template)

**Pedagogy:** Assignment handout → independent work session → presentation of results.

**Deliverable:** Working line-following simulation; short documentation of parameter choices.

**Hardware extension:** Lecturer demonstrates line following on the **Dobot** robot.

**Open questions:**
- Is a competition-style evaluation used, and if so, how is it assessed?
- Is the extended (8-sensor) variant mandatory or optional?

**To do before delivery:**
- Define and write the line-following tutorial and templates for Webots (→ AP4)
- Assemble and test the Dobot hardware

---

### Field Trip

Embedded within Block 2. Students visit an industrial site with AGV deployment in operation.

*Assumption:* Field trip location and date will be coordinated separately; not yet confirmed for the new semester.

---

## 7. Block 3 — Autonomous AGVs with ROS

### Sessions 9–10 (approx. 2 weeks)

### Rationale
ROS (Robot Operating System) is the de-facto standard middleware for autonomous robotics and is ubiquitous in industry. Exposure to ROS gives students literacy in the vocabulary and architecture of modern autonomous systems — even without becoming proficient programmers.

### Revised approach for non-programmers
The previous concept assumed Python knowledge and included student-led coding tasks (publishing topics, writing a ROS node from scratch). These are not feasible for this target group.

**Revised structure:**
- Lecturer and hardware demos take centre stage; students observe, ask questions, and analyse.
- Student activities consist of **running pre-written, pre-configured scripts** and interpreting the output.
- The focus shifts from *building* to *understanding*: what does ROS do here, why does it work this way, what would change if…?
- AP7 revised: students **modify a provided ROS node** (change parameters, add a simple behaviour step) rather than writing one from scratch.

*Assumption:* Pre-configured VMs with a working ROS environment will be provided. Setting up ROS from scratch is not a student task. VM performance with Gazebo must be verified — *not yet confirmed*.

---

### Unit 3.1 — ROS Fundamentals

**Content (lecturer presentation + demo):**
- Why ROS? Motivation, history, and industry relevance
- ROS architecture: nodes, topics, messages, services — conceptual overview
- Packages and workspaces
- **Live demo:** Turtlebot3 sensor data streamed as ROS topics; students observe in real time

**Guided student activity:**
- Open a pre-configured ROS environment on the VM
- Run provided scripts to start and inspect a simulated robot (iRobot Create 3 simulator)
- Use `rostopic echo` and `rqt_graph` to visualise data flow — no coding, command execution only

**Deliverable:** Students can describe the node-topic architecture and identify what data is flowing in a given ROS system.

**To do:** Write a guided activity sheet (→ AP5)

---

### Unit 3.2 — SLAM and Navigation

**Content (lecturer presentation):**
- Localisation approaches: GPS, AprilTags, indoor localisation
- SLAM (Simultaneous Localisation and Mapping): what it does and why it matters
- Path planning: global vs. local planners

**Guided student activity:**
- Launch a pre-configured SLAM session in the **Gazebo** simulator (Turtlebot3 environment provided)
- Drive the robot manually to build a map; observe the map being constructed in RViz
- Then send a navigation goal and observe autonomous path planning in action

**Lecturer demo:**
- SLAM and autonomous navigation with the real **Turtlebot3**

**Planned future addition:** AprilTag localisation demo — *not yet implemented*

**Deliverable:** Students can explain what SLAM is doing in the demo and describe one limitation of the approach.

**To do:** Write a guided activity sheet with pre-configured launch files (→ AP6)

---

### Unit 3.3 — Manipulation

**Content (lecturer demo):**
- Introduction to robot arm control via ROS and MoveIt
- **Live demo:** LoCoBot arm with gripper performing a pick-and-place sequence

**Guided student activity:**
- Open a provided LoCoBot simulation with a pre-written motion script
- Modify clearly marked parameters (target position coordinates, gripper timing) and observe the effect
- This is the AP7 activity: guided modification of an existing ROS node

**Deliverable:** Students document what they changed and how the robot's behaviour differed.

**To do:** Prepare the LoCoBot simulation environment and the parameterised motion script (→ AP7)

---

## 8. Block 4 — AGV Simulation

### Sessions 11–13 (approx. 3 weeks)

### Rationale
Students apply their accumulated understanding by analysing a complete manufacturing simulation. The contrast between classical and AGV-supported production layouts provides a concrete, evaluable scenario that connects technical content to business decision-making.

### Scenario
**Wave manufacturing** — students work with a simulation of a production environment in two configurations:
1. Classical layout (manual transport between stations)
2. AGV-supported layout

They analyse throughput, lead times, WIP (work in progress), and bottlenecks, and draw conclusions about when and why AGV deployment creates value.

### Tool decision — **Plant Simulation (Siemens)** ✅ decided 2026-03-23

Institutional licences for Plant Simulation are available. This resolves Q1.

**Rationale for this choice:**
- GUI-based discrete event simulation — no programming required
- Industry-standard tool widely used in manufacturing and intralogistics
- Strong built-in support for material flow, conveyor systems, and AGV modelling
- Licence barrier removed (institutional access confirmed)

**Alternatives considered and not chosen:**
- *AnyLogic:* Also GUI-based and strong; rejected because Plant Simulation licences are already available, avoiding additional procurement and registration overhead.
- *Webots:* Already known to students but not suited for logistics process simulation and requires coding.
- *Spreadsheet model:* Too simplified for meaningful process analysis.

*Assumption:* Plant Simulation is installed or can be installed on the computer lab VMs. Installation and licence server configuration must be verified before the semester — *not yet confirmed*.

### Open questions
- Individual or group assignment?
- Presentation, written report, or both?

---

## 9. Assessment

### Overview

| Component | Timing | Weight | Contents |
|---|---|---|---|
| **Component 1 — In-semester work** | During semester | **70%** | Webots assignments (Block 2), ROS activities (Block 3), AGV simulation (Block 4) |
| **Component 2 — Business case** | Semester break | **30%** | Market research, business case calculation, Lastenheft, Nutzwertanalyse |

---

### Component 1 — In-Semester Work (70%)

Students are assessed on their hands-on work across the three practical blocks. Each block contributes to this component; the internal weighting between blocks is not yet decided.

| Block | Assignment | Deliverable |
|---|---|---|
| Block 2 | Obstacle avoidance | Working simulation + parameter documentation |
| Block 2 | Labyrinth | Presentation of approach and working demo |
| Block 2 | Line following | Working simulation + short documentation |
| Block 3 | ROS activities | Activity completion + written responses to interpretation questions |
| Block 4 | AGV simulation | Simulation results + analysis report |

**Open question (deferred):** How is the 70% distributed internally across blocks and assignments? Deferred until AP3, AP5, and AP8 are sufficiently defined — the weighting depends on the scope and depth of each assignment.

---

### Component 2 — Business Case (30%)

Submitted during the semester break. The business case is the component most directly aligned with BWL students' existing competencies and professional context.

**Rationale:** BWL students bring core competencies in economics, analysis, and structured argumentation. This component allows them to demonstrate mastery in a format relevant to their career trajectory.

#### Scenario
Students develop a business case for the introduction of an AGV system in a defined intralogistics scenario. The scenario may be provided by the lecturer or chosen by the student — *not yet decided*.

#### Components

| Component | Description |
|---|---|
| **Market research** | Survey of available AGV systems, vendors, and current market trends |
| **Business case calculation** | ROI, payback period, TCO, cost-benefit analysis for the defined scenario |
| **Requirements specification (Lastenheft)** | Structured requirements document for AGV procurement |
| **Utility value analysis (Nutzwertanalyse)** | Weighted scoring of at least two AGV alternatives against defined criteria |

#### Open questions
- Individual or group work?
- Fixed scenario (lecturer-defined) or flexible (student-chosen)?
- Is an introductory handout given at the start of the semester, or only at the end?

**To do:** Create a structured template and grading rubric (→ AP9)

---

## 10. Infrastructure

| Item | Type | Role | Status |
|---|---|---|---|
| **Webots** | Software (free) | AGV simulation in Block 2 | Available; VM performance to be verified |
| **Turtlebot3** | Real hardware | SLAM & navigation demo in Block 3 | Available in lab |
| **LoCoBot** | Real hardware (arm + gripper) | Manipulation demo in Block 3 | Available in lab |
| **Alphabot** | Real hardware | Labyrinth algorithm demo | Available in lab |
| **Dobot** | Real hardware | Line-following demo | Needs assembly and testing |
| **ROS** | Software (free) | Block 3 middleware | Pre-configured VMs planned |
| **Gazebo** | Software (free) | ROS simulation (Turtlebot3) | Pre-configured VMs planned |
| **Computer lab VMs** | Infrastructure | Student workstations for all simulation | Specs and performance not yet confirmed |
| **Plant Simulation (Siemens)** | Software (licensed) | Block 4 wave manufacturing simulation | Institutional licence available; VM installation to be verified |

---

## 11. Open Questions and Next Steps

| # | Question | Priority | Blocks affected |
|---|---|---|---|
| ~~Q1~~ | ~~Which tool for Block 4 AGV simulation?~~ | ✅ Resolved — Plant Simulation (Siemens) | 4 |
| Q2 | Is the business case individual or group work? | 🔴 High | Assessment |
| Q3 | Is the scenario for the business case fixed or student-chosen? | 🔴 High | Assessment |
| Q4 | Can the computer lab VMs run Webots and Gazebo at acceptable performance? | 🟡 Medium | 2, 3 |
| Q4a | How is the 70% distributed internally across Blocks 2, 3, and 4? | ⏸ Deferred — decide once AP3/AP5/AP8 are complete | Assessment |
| Q5 | Is the extended line-following variant (8 sensors) mandatory or optional? | 🟡 Medium | 2 |
| Q6 | Should students deploy their own labyrinth algorithm on the Alphabot? | 🟡 Medium | 2 |
| Q7 | Is a competition format used for line following, and how is it evaluated? | 🟡 Medium | 2 |
| Q8 | How is the business case integrated into the course schedule? | 🟡 Medium | Assessment |
| Q9 | Are all hardware items tested and ready for the new semester? | 🟡 Medium | 2, 3 |
| Q10 | Should prerequisites be formally verified or communicated before the course? | 🟢 Low | All |

---

*Document created 2026-03-23. Revised 2026-03-23: target group confirmed (BWL, no programming background); template-based coding approach adopted; ROS block restructured; business case elevated to primary assessment. Maintained alongside `CLAUDE.md`.*
