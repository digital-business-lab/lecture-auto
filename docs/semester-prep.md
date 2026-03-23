# Semester Preparation Checklist

This checklist covers everything that must be verified, installed, or decided before each new semester begins. Work through it top to bottom — later items often depend on earlier ones.

> **How to use:** Duplicate this checklist at the start of each semester preparation cycle. Track completion per semester (e.g. in a dated copy or via git history). Items marked ⚠️ are known risks from previous semesters or unresolved open questions.

---

## 1. Scheduling and Organisation

- [ ] Confirm semester dates and session schedule
- [ ] Map the four blocks onto the session calendar (see [`docs/course-concept.md`](./course-concept.md) for block durations)
- [ ] Confirm field trip date and location (Block 2)
- [ ] Set deadlines for all assignments and the business case
- [ ] Assign student research topics for Block 1 (industry-specific AGV applications)
- [ ] Communicate prerequisites and course structure to students before the first session

---

## 2. Infrastructure

### Lab Computers (Webots)

- [ ] **Webots:** Verify Webots is installed on all lab computers; run the obstacle avoidance world and confirm acceptable frame rate
- [ ] Communicate download link to students for personal computers ([cyberbotics.com](https://cyberbotics.com))

### Lab Computers (Plant Simulation)

- [ ] **Plant Simulation:** Verify Plant Simulation is installed on all lab computers; configure licence server access; open the wave manufacturing model from `block-04-simulation/models/` and verify it runs

### Virtual Machines (ROS)

> ⚠️ VM performance has not been re-verified since the course concept was revised. All VM-based tools must be tested on the current image before the semester.

- [ ] **ROS:** Deploy pre-configured ROS VM image; verify all launch files and scripts in `block-03-ros/scripts/` run without errors
- [ ] **Gazebo:** Verify the Turtlebot3 Gazebo world loads and runs at acceptable speed on the lab VMs
- [ ] Confirm the number of available student VM seats matches expected enrolment
- [ ] Document software versions in this file under [Current Software Configuration](#current-software-configuration) below

---

## 3. Hardware

- [ ] **Turtlebot3:** Power on and verify ROS connectivity; run a brief SLAM test to confirm sensors and motors are functional
- [ ] **LoCoBot (arm + gripper):** Power on and verify ROS connectivity; test the gripper mechanism; run the provided motion script from `block-03-ros/scripts/`
- [ ] Confirm all hardware is physically present and undamaged
- [ ] Charge or replace batteries as needed

---

## 4. Course Content

### Block 2 — Webots

- [ ] Review assignment sheets in `block-02-webots/assignments/` — update if scenario or requirements have changed
- [ ] Review controller templates in `block-02-webots/templates/` — verify `TODO` gaps are correct and comments are clear
- [ ] Test all Webots world files in `block-02-webots/worlds/` on the lab computers
- [ ] Confirm the labyrinth world is pre-built and the robot starts in the correct position

### Block 3 — ROS

- [ ] Review guided activity sheets in `block-03-ros/assignments/`
- [ ] Test all scripts in `block-03-ros/scripts/` on the current ROS VM image
- [ ] Prepare AprilTag demo materials (if to be included this semester)
- [ ] Review the LoCoBot modification activity (AP7) — confirm parameter ranges are sensible

### Block 4 — Plant Simulation

- [ ] Review the assignment sheet in `block-04-simulation/assignments/`
- [ ] Open and test the wave manufacturing models in `block-04-simulation/models/` on the lab computers
- [ ] Decide (if not yet done): individual or group assignment?
- [ ] Decide (if not yet done): presentation, written report, or both?

### Business Case

- [ ] Review template in `assessment/business-case/`
- [ ] Review grading rubric — adjust point allocation if needed
- [ ] Decide (if not yet done): fixed lecturer scenario or student-chosen scenario?
- [ ] Communicate business case requirements to students at the start of the semester

---

## 5. Open Decisions (resolve before semester start)

These questions from [`docs/course-concept.md`](./course-concept.md) must be answered before the semester begins — they affect content and scheduling:

| Question | Relevant material |
|---|---|
| Individual or group business case? | `assessment/` |
| Fixed or student-chosen business case scenario? | `assessment/` |
| How is the business case integrated into the schedule? | Course schedule |
| Is the extended line-following variant (8 sensors) mandatory or optional? | `block-02-webots/` |
| Is a competition format used for line following, and how is it assessed? | `block-02-webots/` |

---

## 6. After the Semester — Lessons Learned

At the end of each semester, record the following here (or in a dated `docs/lessons-YYYY.md` file):

- [ ] Which assignments caused the most difficulty? What was the likely cause?
- [ ] Did any VM or hardware issues disrupt sessions? How were they resolved?
- [ ] Were time allocations for each block accurate? What needs more or less time?
- [ ] Were the code templates at the right difficulty level?
- [ ] Student feedback summary (if collected)
- [ ] Update `CLAUDE.md` decision log with any changes to the course concept

---

## Current Software Configuration

> Update this table after each semester's infrastructure setup.

### Lab Computers

| Software | Version | Last verified | Notes |
|---|---|---|---|
| Webots | — | Not yet verified for revised concept | Native install; no VM |
| Plant Simulation | — | Not yet verified | Native install; licence server config required |

### Virtual Machines

| Software | Version | Last verified | Notes |
|---|---|---|---|
| ROS | — | Not yet verified for revised concept | — |
| Gazebo | — | Not yet verified for revised concept | — |

---

*Created 2026-03-23. Update this file after each semester's preparation cycle.*
