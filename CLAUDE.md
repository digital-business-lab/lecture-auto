# CLAUDE.md — Project Memory: Autonomous Logistics Systems and IoT

> **Always read this file first** before starting any work on this project.
> This is a living document. Update it after every significant decision or session.
> Last updated: 2026-03-23 (AP1 completed; course-concept.md created)

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
- **Planned measures:**
  - Provide the labyrinth world pre-built, so students focus on AGV behaviour rather than environment modelling.
  - Provide structured introductory tutorials.
  - Simplify VM setup or add a step-by-step installation guide.
- **Assumption:** Difficulty stems from Webots unfamiliarity, not from the algorithm itself — *not yet validated*.
- **Status:** ⏳ Open — material to be created (→ AP2, AP3)

### 6.2 ROS Unit Needs More Depth

- **Problem:** The ROS block is outlined but hands-on assignments are not fully developed.
- **Planned measures:**
  - Detailed assignment sheets for ROS basics, SLAM, and navigation.
  - Integrate AprilTag demo.
  - Add a mini-project: programming a ROS node.
- **Assumption:** Students have basic Python knowledge; ROS-specific concepts are new to them.
- **Status:** ⏳ Open — assignments to be specified (→ AP5, AP6, AP7)

### 6.3 AGV Simulation Assignment Too Vague

- **Problem:** The wave manufacturing simulation task has no clear problem statement, requirements, or evaluation criteria.
- **Planned measures:**
  - Write a concrete assignment with scenario, requirements, and a grading rubric.
  - Decide on the simulation tool to be used.
- **Open question:** Should students use Webots, a custom Python simulation, or a dedicated logistics simulation tool (e.g. AnyLogic, Plant Simulation)?
- **Status:** ⏳ Open — assignment to be written (→ AP8)

### 6.4 Business Case Not Structured

- **Problem:** The business case is listed as an additional assessment but has no template, rubric, or clear scope.
- **Planned measures:**
  - Create a template document.
  - Define a grading rubric.
  - Decide: mandatory or optional assessment?
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

---

## 8. Work Packages

Planned work items, updated continuously.

| ID | Description | Status |
|---|---|---|
| AP1 | Revised course concept as a structured document | ✅ Done — `docs/course-concept.md` |
| AP2 | Webots introduction tutorial (VM setup, first robot, first controller) | ⏳ Open |
| AP3 | Revised labyrinth assignment (pre-built world + clear task description) | ⏳ Open |
| AP4 | Line-following tutorial for Webots (basic + extended) | ⏳ Open |
| AP5 | ROS assignment sheet: fundamentals + environment setup | ⏳ Open |
| AP6 | ROS assignment sheet: SLAM and navigation in Gazebo | ⏳ Open |
| AP7 | ROS mini-project: define and develop a custom ROS node | ⏳ Open |
| AP8 | AGV simulation assignment: wave manufacturing scenario | ⏳ Open |
| AP9 | Business case template + grading rubric | ⏳ Open |
| AP10 | Finalise overall concept and align with new semester schedule | ⏳ Open |

---

## 9. Tools and Technologies

| Tool | Role in the course |
|---|---|
| **Webots** | Simulation of classical AGVs (obstacle avoidance, labyrinth, line following) |
| **Alphabot** | Physical hardware demo for labyrinth algorithms |
| **Dobot** | Physical hardware demo for line following |
| **ROS** | Middleware for autonomous AGVs (fundamentals, SLAM, navigation, manipulation) |
| **Gazebo** | Simulator for ROS assignments (Turtlebot 3/4) |
| **Create 3 Simulator** | First ROS experiments |
| **LoCoBot** | Manipulation: demo + Python simulation |
| **Turtlebot 3/4** | SLAM & navigation demo (real hardware) |

---

*Created by Claude (Anthropic) in collaboration with the lecturer — 2026-03-23*
