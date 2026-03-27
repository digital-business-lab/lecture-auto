# Course Concept: Autonomous Logistics Systems and IoT

> **Status:** Working draft — revised 2026-03-23
> This document is the authoritative description of the course structure, content, and pedagogy.
> It supersedes the informal notes from the previous semester.
>
> **Detail lives in the block READMEs.** This file provides the overall framing; links below point to the full per-block content.

---

## 1. Course Overview

| Field | Detail |
|---|---|
| **Title** | Autonomous Logistics Systems and IoT |
| **Level** | Master |
| **Topic focus** | Automated Guided Vehicles (AGVs) in intralogistics |
| **Format** | Lecture + hands-on labs (simulation) |
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
| 2 | Classical AGVs with Webots | 3–7 | 5 weeks | part of 70% |
| 3 | Autonomous AGVs with ROS | 8–9 | 2 weeks | part of 70% |
| 4 | AGV Simulation | 10–12 | 3 weeks | part of 70% |
| + | Business Case | semester break | — | 30% |

**Assessment structure:**
- **Component 1 (70%) — in-semester:** Hands-on assignments across Blocks 2, 3, and 4 (Webots tasks, ROS activities, Plant Simulation). Submitted and evaluated during the semester.
- **Component 2 (30%) — semester break:** Business case. Submitted after the semester ends.

*Open question:* How is the 70% distributed internally across Blocks 2, 3, and 4? Not yet decided.

---

## 5. Block 1 — Organisation & Foundations

Sessions 1–2 (3 hours each). Covers the organisational introduction and AGV technology foundations. Group work in both sessions: AGV epochs, suitability of alternatives, and industry-specific applications.

→ **Full detail:** [`block-01-foundations/README.md`](../block-01-foundations/README.md)

---

## 6. Block 2 — Classical AGVs with Webots

Sessions 3–7 (approx. 5 weeks). Students use the Webots robot simulator for two graded assignments: labyrinth solving (Sessions 4–5, 6 h) and line following (Session 7). All coding uses pre-written templates with `TODO` gaps.

→ **Full detail:** [`block-02-webots/README.md`](../block-02-webots/README.md)

---

## 7. Block 3 — Autonomous AGVs with ROS

Sessions 8–9 (approx. 2 weeks). Two interleaved themes: (1) the technical building blocks of autonomous AGVs (sensors, dead reckoning, landmark localisation, SLAM, path planning) and (2) ROS as the middleware that integrates these components. Content is delivered through lecturer presentations and hardware demos; student activities use pre-written scripts and pre-configured VMs. The complete TurtleBot3 workflow (simulation in Gazebo → live hardware demo) serves as a unifying red thread. Students observe and run — they do not write ROS code.

→ **Full detail:** [`block-03-ros/README.md`](../block-03-ros/README.md)

---

## 8. Block 4 — AGV Simulation

Sessions 10–12 (approx. 3 weeks). Students simulate a shaft manufacturing scenario in two configurations (classical vs. AGV-supported) using **Plant Simulation (Siemens)**. GUI-based; no programming required. Institutional licence available.

→ **Full detail:** [`block-04-simulation/README.md`](../block-04-simulation/README.md)

---

## 9. Assessment

Two-component grading: 70% in-semester (Blocks 2–4) + 30% business case (semester break). The business case covers market research, cost-benefit analysis, a requirements specification (Lastenheft), and a utility value analysis (Nutzwertanalyse).

→ **Full detail:** [`assessment/README.md`](../assessment/README.md)

---

## 10. Infrastructure

| Item | Type | Role | Status |
|---|---|---|---|
| **Webots** | Software (free) | AGV simulation in Block 2 | Available; VM performance to be verified |
| **Turtlebot3** | Real hardware | SLAM & navigation demo in Block 3 | Available in lab |
| **LoCoBot** | Real hardware (arm + gripper) | Manipulation demo in Block 3 | Available in lab |
| **ROS** | Software (free) | Block 3 middleware | Pre-configured VMs planned |
| **Gazebo** | Software (free) | ROS simulation (Turtlebot3) | Pre-configured VMs planned |
| **Computer lab VMs** | Infrastructure | Student workstations for all simulation | Specs and performance not yet confirmed |
| **Plant Simulation (Siemens)** | Software (licensed) | Block 4 shaft manufacturing simulation | Native install on lab computers |

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
| Q7 | Is a competition format used for line following, and how is it evaluated? | 🟡 Medium | 2 |
| Q8 | How is the business case integrated into the course schedule? | 🟡 Medium | Assessment |
| Q9 | Are all hardware items tested and ready for the new semester? | 🟡 Medium | 3 |
| Q10 | Should prerequisites be formally verified or communicated before the course? | 🟢 Low | All |

---

*Document created 2026-03-23. Revised 2026-03-23: target group confirmed (BWL, no programming background); template-based coding approach adopted; ROS block restructured; business case elevated to primary assessment. Block detail moved to per-block READMEs 2026-03-23.*
