# Block 2 — Classical AGVs with Webots

Hands-on simulation phase using the Webots robot simulator. All student activities use pre-written code templates — students complete marked `TODO` sections, they do not write code from scratch.

## Workflow Overview

Block 2 follows four sessions:

| Session | Activity | Graded |
|---|---|---|
| 3 | Webots Tutorials 1–7 — model a simple robot ([Webots User Guide](https://cyberbotics.com/doc/guide/tutorials)) | No |
| 4 | Labyrinth — complete a maze-solving controller; present results | **Yes** |
| 5 | Sensor extension — add sensors to the robot in preparation for line following | No |
| 6 | Line following — complete a line-tracking controller (basic + extended) | **Yes** |

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

See [`docs/course-concept.md`](../docs/course-concept.md#6-block-2--classical-agvs-with-webots) for the full pedagogical concept.

## Open Development Tasks (one-time)

> These are internal preparation tasks — not student-facing.

- [ ] **Labyrinth dimensions check:** Verify that the pre-built labyrinth world (`worlds/labyrinth.wbt`) is dimensionally compatible with the robot built in the Webots User Guide Tutorials 1–7. Passage widths and robot footprint must match so students can reuse their tutorial robot directly.
- [ ] **Line-following world:** Create the Webots world file for the line-following assignment (`worlds/line_track.wbt`) — standard track for the 4-sensor variant. Extended version (`worlds/line_track_extended.wbt`) with colour-varying track follows as part of AP4.
