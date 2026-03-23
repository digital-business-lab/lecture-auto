# Block 2 — Classical AGVs with Webots

**Sessions 3–6 · Duration: approx. 4 weeks · 3 hours per session**

This block introduces hands-on AGV simulation using [Webots](https://cyberbotics.com), a free and open-source robot simulator. You will model a robot, program its behaviour, and solve two graded assignments — all without prior programming experience, using pre-written code templates.

---

## Sessions Overview

All assignments use **pre-written code templates** — you fill in the marked `TODO` sections. You never write code from scratch. Every non-trivial line is explained with inline comments.

| Session | Activity | Graded |
|---|---|---|
| 3 | Webots Tutorials 1–7 — model a simple robot | No |
| 4 | Labyrinth — implement and present a maze-solving controller | **Yes** |
| 5 | Sensor extension — add sensors to the robot | No |
| 6 | Line following — implement a line-tracking controller | **Yes** |

---

## Session 3 — Webots Tutorials 1–7 (3 h)

**Not graded — introductory**

Before the first assignment, you work through the official [Webots User Guide Tutorials 1–7](https://cyberbotics.com/doc/guide/tutorials). These tutorials guide you step by step through modelling a simple robot and writing your first controller.

By the end of Session 3, you will:

- [ ] Know how to open and navigate Webots
- [ ] Have built and run a simple robot model yourself
- [ ] Understand how a controller communicates with a simulated robot

!!! tip "Work at your own pace"
    The tutorials are self-paced and should be completed before the first assignment session. Bring questions to the next session.

---

## Session 4 — Labyrinth (3 h) *(graded)*

**Goal:** Implement a maze-solving strategy and present your results.

You receive a **pre-built labyrinth world** and a **controller template**. Your task is to complete the maze-solving logic gaps in the template (e.g. wall-following decision rules), refine your algorithm, and present your approach and a working demo to the group.

**What you hand in:**

- [ ] A working Webots simulation in which your robot navigates the labyrinth
- [ ] A short presentation of your approach and results

!!! note "Assessment"
    This assignment is graded and counts towards the 70% in-semester component.

---

## Session 5 — Sensor Extension (3 h)

**Not graded — bridging session**

Before the line-following assignment, you extend your robot with additional ground sensors directly in Webots. You verify the sensor readings in the simulation console.

This session prepares you technically for Session 6 — no deliverable is required.

---

## Session 6 — Line Following (3 h) *(graded)*

**Goal:** Implement line-tracking behaviour using provided templates.

**Basic (all students):**

- [ ] Complete the template controller for line following with 4 sensors on a standard track
- [ ] Test and tune sensor weights and speed parameters

**Extended (optional):**

- [ ] Adapt the controller for 8 sensors and tracks with varying colours

**What you hand in:**

- [ ] A working line-following simulation
- [ ] Short documentation of your parameter choices

!!! note "Assessment"
    This assignment is graded and counts towards the 70% in-semester component.

---

## Block 2 Materials

| Material | Description | Where to find |
|---|---|---|
| Lecture slides | Webots introduction and AGV control concepts | Moodle |
| Webots tutorials | Official guided tutorials 1–7 | [cyberbotics.com/doc/guide/tutorials](https://cyberbotics.com/doc/guide/tutorials) |
| Assignment sheets | Labyrinth + line following | Distributed in session |
| Code templates | Pre-written controllers with `TODO` gaps | Distributed in session |
