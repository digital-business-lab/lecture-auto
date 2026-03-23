# Block 2 — Classical AGVs with Webots

Hands-on simulation phase using the Webots robot simulator. All student activities use pre-written code templates — students complete marked `TODO` sections, they do not write code from scratch.

## Rationale

Webots provides a free, cross-platform robot simulator suitable for teaching AGV fundamentals without requiring dedicated hardware. Hands-on work in simulation makes abstract concepts tangible for students without a programming background.

## Coding Approach — Template-based ("Light Coding")

- A **complete, working controller** is provided as the starting point.
- Sections encoding core logic (decision thresholds, sensor weights, state transitions) are replaced with **clearly marked `TODO` gaps**.
- Students read the surrounding code (with explanations) to understand *what* it does, then complete the gaps based on the assignment instructions.
- Students never write a controller from scratch.

This approach preserves the hands-on learning benefit while removing the barrier of syntax and language unfamiliarity. It also allows the lecturer to control complexity precisely.

*Assumption:* Even with templates, some students will find Python syntax confusing. Templates must therefore include extensive inline comments explaining every non-trivial line. This has not been tested yet.

## Software

Webots is available for Windows, Linux, and macOS. It is free and open-source (Apache 2.0).

- **Lab computers:** Webots is pre-installed — students open it directly.
- **Personal computers:** Download from [cyberbotics.com](https://cyberbotics.com).

*VM performance with Webots must be verified before the semester begins — not yet confirmed.*

---

## Sessions Overview

| Session | Activity | Graded |
|---|---|---|
| 3 | Webots Tutorials 1–7 — model a simple robot ([Webots User Guide](https://cyberbotics.com/doc/guide/tutorials)) | No |
| 4 | Labyrinth — complete a maze-solving controller; present results | **Yes** |
| 5 | Sensor extension — add sensors to the robot in preparation for line following | No |
| 6 | Line following — complete a line-tracking controller (basic + extended) | **Yes** |

---

## Session 3 — Webots Tutorials 1–7 (3 h, not graded)

**Goal:** Students learn the Webots environment by following the official guided tutorials. They model a simple robot from scratch and understand the simulation–controller relationship before working on graded assignments.

### Tasks
1. Set up the Webots environment on the provided VM
2. Work through [Webots User Guide Tutorials 1–7](https://cyberbotics.com/doc/guide/tutorials) step by step:
   - Tutorial 1: Your first simulation in Webots
   - Tutorial 2: Modification of the environment
   - Tutorial 3: Appearance
   - Tutorial 4: More about controllers
   - Tutorial 5: Road and vehicles
   - Tutorial 6: 4-wheeled robot
   - Tutorial 7: Your first Webots application
3. By the end, students have a working, self-modelled robot with a basic controller

**Deliverable:** None (ungraded introduction). Students are expected to complete the tutorials before the first graded assignment.

---

## Session 4 — Labyrinth (3 h, graded)

**Goal:** Students implement a maze-solving strategy using sensor data and control logic by completing a provided template.

### Tasks
1. Receive a **pre-built labyrinth world** in Webots (students do not model the environment)
2. Receive a controller template implementing the basic robot loop; complete the maze-solving logic gaps (e.g. wall-following decision rules)
3. Refine and test the algorithm within the simulation
4. Present approach and results to the group

**Pedagogy:** Independent work phase (approx. 2 sessions) followed by group presentations.

**Deliverable:** Presentation of maze-solving approach; working simulation demo. *(Graded — part of the 70% in-semester component)*

---

## Session 5 — Sensor Extension (3 h, not graded)

**Goal:** Students extend the robot built in earlier sessions with additional sensors in preparation for the line-following assignment.

### Tasks
1. Add ground/light sensors to the existing robot model in Webots
2. Verify sensor readings in the simulation console
3. Understand how sensor data will be used for line-following control

**Deliverable:** None (ungraded). The extended robot serves as the starting point for Session 6.

---

## Session 6 — Line Following (3 h, graded)

**Goal:** Students implement line-tracking behaviour at two complexity levels using provided templates.

### Tasks

*Basic (all students):*
1. Complete a template controller for line following with 4 sensors on a standard track
2. Test and tune sensor weights and speed parameters

*Extended (optional or for advanced students):*
3. Adapt the controller for 8 sensors and tracks with varying colours (additional `TODO` sections in an extended template)

**Pedagogy:** Assignment handout → independent work session → presentation of results.

**Deliverable:** Working line-following simulation; short documentation of parameter choices. *(Graded — part of the 70% in-semester component)*

### Open Questions
- Is a competition-style evaluation used, and if so, how is it assessed?
- Is the extended (8-sensor) variant mandatory or optional?

---

## Field Trip

Embedded within Block 2. Students visit an industrial site with AGV deployment in operation.

*Assumption:* Field trip location and date will be coordinated separately; not yet confirmed for the new semester.

---

## Folder Structure

| Folder | Contents |
|---|---|
| `assignments/` | Assignment sheets (PDF/Markdown) handed out to students |
| `templates/` | Pre-written Webots controller templates with `TODO` gaps |
| `worlds/` | Webots world files (pre-built environments) |

## Assignments and Templates

| Session | Assignment | Sheet | Template | World | Status |
|---|---|---|---|---|---|
| 4 | Labyrinth | `assignments/labyrinth.md` | `templates/labyrinth_template.py` | `worlds/labyrinth.wbt` | ⏳ To do (AP3) |
| 6 | Line following (basic) | `assignments/line-following.md` | `templates/line_following_template.py` | `worlds/line_track.wbt` | ⏳ To do (AP4) |
| 6 | Line following (extended) | `assignments/line-following.md` | `templates/line_following_extended_template.py` | `worlds/line_track_extended.wbt` | ⏳ To do (AP4) |

---

## Open Development Tasks (one-time)

> These are internal preparation tasks — not student-facing.

- [ ] **Labyrinth dimensions check:** Verify that the pre-built labyrinth world (`worlds/labyrinth.wbt`) is dimensionally compatible with the robot built in the Webots User Guide Tutorials 1–7. Passage widths and robot footprint must match so students can reuse their tutorial robot directly.
- [ ] **Line-following world:** Create the Webots world file for the line-following assignment (`worlds/line_track.wbt`) — standard track for the 4-sensor variant. Extended version (`worlds/line_track_extended.wbt`) with colour-varying track follows as part of AP4.
