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

| Session | Activity | Graded | Details |
|---|---|---|---|
| 3 | Webots Tutorials 1–7 — model a simple robot ([Webots User Guide](https://cyberbotics.com/doc/guide/tutorials)) | No | [session-03.md](session-03.md) |
| 4 | Labyrinth — complete a maze-solving controller; present results | **Yes** | [session-04.md](session-04.md) |
| 5 | Sensor extension — add sensors to the robot in preparation for line following | No | [session-05.md](session-05.md) |
| 6 | Line following — complete a line-tracking controller (basic + extended) | **Yes** | [session-06.md](session-06.md) |

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
