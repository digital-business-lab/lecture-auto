# CLAUDE.md — Project Memory: Autonomous Logistics Systems and IoT

> **Always read this file first** before starting any work on this project.
> This is a living document. Update it after every significant decision or session.
> Last updated: 2026-03-23 (target group clarified; template-based coding approach decided)

---

## 1. Project Overview

| Field | Content |
|---|---|
| **Course** | Autonomous Logistics Systems and IoT |
| **Level** | Master |
| **Topic** | Use of Automated Guided Vehicles (AGVs) in intralogistics |
| **GitHub Organisation** | digital-business-lab |
| **Repository** | lecture-auto |
| **URL** | https://github.com/digital-business-lab/lecture-auto |
| **Purpose** | Accompanying material for the course (assignments, tutorials, simulations, documents) |
| **Target group** | Master's students in business administration (BWL) — **no programming background** |

### Available Infrastructure

| Item | Type | Notes |
|---|---|---|
| **Turtlebot3** | Real hardware | SLAM, navigation demos in Block 3 |
| **LoCoBot** | Real hardware | Robot arm with gripper; manipulation demo in Block 3 |
| **Computer lab VMs** | Virtual machines | Student workstations; Webots and ROS run here; specs not yet confirmed |

---

## 2. Project Goals

This repository provides structured, version-controlled material to accompany the course across multiple semesters. The three primary goals are:

1. **Refine the course concept** based on lessons learned from the previous semester.
2. **Create accompanying material** — assignment sheets, tutorials, scripts, simulation files.
3. **Document decisions** regarding pedagogy, tools, and content so that future iterations can build on past reasoning.

---

## 3. Working Conventions

### 3.1 Language

| Context | Language |
|---|---|
| Communication with the lecturer | German |
| All files, documentation, code, and comments in the repository | English |

### 3.2 Repository Structure

| Path | Purpose |
|---|---|
| `README.md` | Slim overview and navigation hub only — no detailed content |
| `CLAUDE.md` | This file; always read first; the single source of truth for project state |
| `docs/*.md` | Detailed documentation for specific topics; linked from `README.md` |

**Rule:** Never put detailed content directly into `README.md`. Always put it in the appropriate `docs/*.md` file and link from `README.md`.

### 3.3 Git Conventions

- **Commit messages:** English, imperative mood, conventional commits format
  - `feat: add Webots obstacle avoidance tutorial`
  - `fix: correct sensor count in line-following assignment`
  - `docs: update decision log in CLAUDE.md`
- **Branches:** Feature branches for larger work packages; direct commits to `main` for documentation updates.
- **Commit scope:** One logical change per commit; keep commits small and reviewable.

### 3.4 Maintaining This File

`CLAUDE.md` is a living document. The following rules apply at the end of every session:

- **Update after every significant decision** — if a technology choice, architectural direction, naming convention, or workflow is agreed upon, add or revise the relevant entry before the session ends.
- **Record the rationale, not just the outcome** — note briefly *why* a decision was made (constraint, trade-off, experiment result), so future sessions can judge whether it still holds.
- **Remove or flag outdated entries** — if a previous decision is superseded, either update the entry or mark it `(superseded)` with the replacement noted.
- **Keep entries concise** — one to two sentences per item; link to the relevant `docs/*.md` file for deeper context.

---

## 4. Scientific and Self-Critical Working Practice

All design decisions, technology choices, and implementation proposals must follow a scientific, self-critical approach:

- **State assumptions explicitly** — before proposing a solution, name the assumptions it rests on (e.g. load estimates, student skill level, hardware availability).
- **Consider alternatives** — for non-trivial decisions, briefly acknowledge at least one alternative and explain why it was not chosen.
- **Identify open questions and risks** — flag anything not yet validated (e.g. *"untested with actual hardware"*, *"student Python proficiency assumed at beginner level"*).
- **Prefer reversible decisions** — when two options are comparable, prefer the one that is easier to change later.
- **Distinguish fact from assumption** — use precise language: *"the sensor measures …"* (fact) vs. *"the sensor is expected to measure …"* (assumption).

---

## 5. Course Structure (as of last semester)

### Block 1 — Organisation & Foundations (Sessions 1–2)

- Course overview and topic assignment
- History and modern applications of AGVs
- AGV technology: navigation/guidance, safety, fleet management, vehicle types, environment, future trends
- **Pedagogy:** Lecturer presentation + student research (industry-specific aspects)
- **Decision (2026-03-23):** Terminology definition section removed — low learning benefit, high time cost.

### Block 2 — Classical AGVs with Webots (Sessions 3–8, approx. 6 weeks)

Hands-on phase using the **Webots** simulation environment and physical hardware.

| Assignment | Description |
|---|---|
| **Obstacle avoidance** | Model a custom robot in Webots; implement an obstacle avoidance controller |
| **Labyrinth** | Develop a maze-solving algorithm; present results; hardware demo on the Alphabot |
| **Line following** | Line tracking in Webots (basic: 4 sensors; extended: 8 sensors, varying colours); hardware demo with Dobot |

- **Field trip:** Embedded in this block.

### Block 3 — Autonomous AGVs with ROS (Sessions 9–10, approx. 2 weeks)

Introduction to **ROS (Robot Operating System)** as a robotics middleware.

| Unit | Content |
|---|---|
| **ROS Fundamentals** | Why ROS? Architecture, packages, topics; demo with Turtlebot sensor data; hands-on with Create 3 simulator |
| **SLAM & Navigation** | Localisation (GPS, AprilTags, indoor); SLAM; path planning; Gazebo simulator (Turtlebot 3/4); live demo with real Turtlebot |
| **Manipulation** | Demo: LoCoBot robot arm; hands-on: Python motion sequence in LoCoBot simulator |

### Block 4 — AGV Simulation (Sessions 11–13, approx. 3 weeks)

- **Topic:** Simulation of wave manufacturing — classical vs. AGV-supported
- Sequence: Assignment handout → independent work → (likely: presentation)
- **Open question:** Which simulation tool will be used? Not yet decided.

### Additional Assessment — Business Case

- Market research and information gathering
- Business case calculation
- Requirements specification (Lastenheft)
- Utility value analysis (Nutzwertanalyse)

---

## 6. Known Weaknesses and Improvement Areas

Issues identified from last semester, all currently open.

### 6.1 Webots Onboarding Too Difficult

- **Problem:** Students struggled significantly with getting started in Webots; the processing time for the labyrinth assignment had to be extended.
- **Root cause (revised):** Now confirmed that students have *no programming background*. The difficulty was almost certainly caused by the combination of an unfamiliar tool *and* unfamiliar programming — not Webots alone.
- **Planned measures:**
  - Provide the labyrinth world pre-built (decided 2026-03-23).
  - Provide all assignments as pre-written code templates with clearly marked gaps; students fill in logic, never write from scratch (decided 2026-03-23 → see 7. Decision Log).
  - Structured step-by-step tutorial for VM setup and first Webots interaction (→ AP2).
- **Status:** ⏳ Open — templates and tutorial to be created (→ AP2, AP3, AP4)

### 6.2 ROS Unit Needs Fundamental Restructuring

- **Problem:** The ROS block assumed Python knowledge that students do not have. A mini-project to write a custom ROS node from scratch is not feasible for this target group.
- **Revised approach:**
  - Shift student activities from *writing code* to *running pre-written scripts and interpreting results*.
  - Focus on conceptual understanding: what ROS does, why it matters, how its parts fit together.
  - Lecturer and hardware demos (Turtlebot3, LoCoBot) become the primary learning medium.
  - AP7 (ROS mini-project) revised: students modify a provided ROS node rather than creating one from scratch.
- **Status:** ⏳ Open — assignments to be redesigned (→ AP5, AP6, AP7)

### 6.3 AGV Simulation Assignment Too Vague

- **Problem:** The wave manufacturing simulation task has no clear problem statement, requirements, or evaluation criteria.
- **Planned measures:**
  - Write a concrete assignment with scenario, requirements, and a grading rubric.
  - Decide on the simulation tool to be used.
- **Tool decision (2026-03-23):** Plant Simulation (Siemens) — institutional licences available; GUI-based, no coding required. Installation on VMs still to be verified.
- **Status:** ⏳ Open — assignment to be written (→ AP8)

### 6.4 Business Case Not Structured — and Underweighted

- **Problem:** The business case is listed as an *additional* assessment but is actually the most appropriate form of assessment for BWL students. It is not yet structured.
- **Revised direction:** Elevate the business case to a primary (mandatory) assessment. BWL students bring relevant core competencies here (economics, analysis, decision-making).
- **Planned measures:**
  - Create a structured template document.
  - Define a grading rubric.
  - Decide on integration into the course schedule.
- **Open question:** Integration into the course flow (standalone vs. embedded in Block 4) not yet decided.
- **Status:** ⏳ Open — concept and template pending (→ AP9)

---

## 7. Decision Log

All significant decisions are recorded here so that the reasoning remains traceable across sessions.

| Date | Decision | Rationale |
|---|---|---|
| 2026-03-23 | Introduced `CLAUDE.md` as central project memory | Enables persistent, versioned documentation across sessions; survives context resets |
| 2026-03-23 | Removed terminology definition section from Block 1 | Low learning benefit relative to the time cost for students |
| 2026-03-23 | Labyrinth world will be provided pre-built | Students should focus on AGV algorithm, not Webots environment modelling |
| 2026-03-23 | All repository files and documentation in English | Consistent with academic and open-source norms; code is also English |
| 2026-03-23 | `README.md` kept as navigation hub only; detailed content in `docs/*.md` | Avoids README bloat; makes content discoverable and linkable |
| 2026-03-23 | Commit messages in English, conventional commits format | Consistency, tooling compatibility (changelogs, semantic release) |
| 2026-03-23 | Course concept written as `docs/course-concept.md` in Markdown | Stays version-controlled in the repo; no external tool dependency; linked from `README.md` |
| 2026-03-23 | Target group confirmed: BWL Master's students, no programming background | Changes the entire approach to student-facing assignments; all previous assumptions of Python knowledge are invalid |
| 2026-03-23 | Webots assignments use template-based coding ("Light Coding") | Students complete pre-written code templates with clearly marked gaps; no code written from scratch; reduces cognitive load while preserving hands-on learning |
| 2026-03-23 | ROS block restructured: demo-first, scripts provided, no from-scratch coding | Without programming background, student-led ROS coding is not feasible; understanding and evaluation replace implementation |
| 2026-03-23 | Business case elevated to primary (mandatory) assessment | BWL students' core competencies align with this format; it was underweighted as an "additional" assessment |
| 2026-03-23 | AP7 revised: students modify a provided ROS node, not create one from scratch | Writing a ROS node from scratch is unrealistic without programming background; guided modification achieves similar learning outcome |
| 2026-03-23 | Block 4 simulation tool: Plant Simulation (Siemens) | Institutional licences available; GUI-based, no coding required, industry-standard for manufacturing simulation; preferred over AnyLogic (no additional licence procurement needed) |

---

## 8. Work Packages

Planned work items, updated continuously.

| ID | Description | Status |
|---|---|---|
| AP1 | Revised course concept as a structured document | ✅ Done — `docs/course-concept.md` |
| AP2 | Webots introduction tutorial (VM setup, first robot, first controller) | ⏳ Open |
| AP3 | Revised labyrinth assignment (pre-built world + clear task description) | ⏳ Open |
| AP4 | Line-following tutorial for Webots (basic + extended) | ⏳ Open |
| AP5 | ROS guided activity: fundamentals + running provided scripts | ⏳ Open |
| AP6 | ROS guided activity: SLAM and navigation in Gazebo (pre-configured) | ⏳ Open |
| AP7 | ROS guided activity: modify a provided ROS node (no from-scratch coding) | ⏳ Open |
| AP8 | AGV simulation assignment: wave manufacturing scenario | ⏳ Open |
| AP9 | Business case template + grading rubric | ⏳ Open |
| AP10 | Finalise overall concept and align with new semester schedule | ⏳ Open |

---

## 9. Tools and Technologies

| Tool | Role in the course |
|---|---|
| **Webots** | Simulation of classical AGVs (obstacle avoidance, labyrinth, line following) — students use provided templates |
| **Turtlebot3** | Real hardware; SLAM & navigation demo in Block 3 |
| **LoCoBot** | Real hardware with gripper arm; manipulation demo in Block 3 |
| **Alphabot** | Physical hardware demo for labyrinth algorithms |
| **Dobot** | Physical hardware demo for line following |
| **ROS** | Middleware for autonomous AGVs; students run provided scripts, do not write from scratch |
| **Gazebo** | Simulator for ROS activities (Turtlebot3); pre-configured environments provided |
| **Create 3 Simulator** | First guided ROS experiments |
| **Plant Simulation (Siemens)** | Block 4 wave manufacturing simulation; institutional licence available; installation on VMs to be verified |
| **Computer lab VMs** | Student workstations; all simulation software runs here; VM specs to be confirmed |

---

*Created by Claude (Anthropic) in collaboration with the lecturer — 2026-03-23*
