# Block 2 — Classical AGVs with Webots

**Sessions 3–8 · Duration: approx. 6 weeks**

This block introduces hands-on AGV simulation using [Webots](https://cyberbotics.com), a free and open-source robot simulator. You will model a robot, program its behaviour, and solve two graded assignments — all without prior programming experience, using pre-written code templates.

---

## How Block 2 Works

All assignments use **pre-written code templates** — you fill in the marked `TODO` sections. You never write code from scratch. Every non-trivial line is explained with inline comments.

Block 2 follows four steps:

| Step | Activity | Graded |
|---|---|---|
| 1 | Webots Tutorials 1–7 — model a simple robot | No |
| 2 | Labyrinth — implement and present a maze-solving controller | **Yes** |
| 3 | Sensor extension — add sensors to the robot | No |
| 4 | Line following — implement a line-tracking controller | **Yes** |

---

## Step 1 — Webots Tutorials 1–7

**Not graded — introductory**

Before the first assignment, you work through the official [Webots User Guide Tutorials 1–7](https://cyberbotics.com/doc/guide/tutorials). These tutorials guide you step by step through modelling a simple robot and writing your first controller.

By the end of Step 1, you will:

- [ ] Know how to open and navigate Webots
- [ ] Have built and run a simple robot model yourself
- [ ] Understand how a controller communicates with a simulated robot

!!! tip "Work at your own pace"
    The tutorials are self-paced and should be completed before the first assignment session. Bring questions to the next session.

---

## Step 2 — Labyrinth *(graded)*

**Goal:** Implement a maze-solving strategy and present your results.

You receive a **pre-built labyrinth world** and a **controller template**. Your task is to complete the maze-solving logic gaps in the template (e.g. wall-following decision rules), refine your algorithm, and present your approach and a working demo to the group.

**What you hand in:**

- [ ] A working Webots simulation in which your robot navigates the labyrinth
- [ ] A short presentation of your approach and results

**Hardware demo:** After the assignment, the lecturer demonstrates the same algorithm running on a physical **Alphabot** robot. You compare simulation and real-world behaviour.

!!! note "Assessment"
    This assignment is graded and counts towards the 70% in-semester component.

---

## Step 3 — Sensor Extension

**Not graded — bridging step**

Before the line-following assignment, you extend your robot with additional ground sensors directly in Webots. You verify the sensor readings in the simulation console.

This step prepares you technically for Step 4 — no deliverable is required.

---

## Step 4 — Line Following *(graded)*

**Goal:** Implement line-tracking behaviour using provided templates.

**Basic (all students):**

- [ ] Complete the template controller for line following with 4 sensors on a standard track
- [ ] Test and tune sensor weights and speed parameters

**Extended (optional):**

- [ ] Adapt the controller for 8 sensors and tracks with varying colours

**What you hand in:**

- [ ] A working line-following simulation
- [ ] Short documentation of your parameter choices

**Hardware demo:** The lecturer demonstrates line following on a physical **Dobot** robot.

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
