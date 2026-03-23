# Session 6 — Line Following Assignment

**Duration: 3 hours · Graded**

---

## Goal

Implement line-tracking behaviour for a simulated AGV using provided code templates.

---

## Variants

### Basic (all students)

- [ ] Complete the template controller for line following with **4 sensors** on a standard track
- [ ] Test and tune sensor weights and speed parameters until the robot reliably follows the line

### Extended (optional)

- [ ] Adapt the controller for **8 sensors** and tracks with varying colours

---

## Deliverables

- [ ] A working line-following simulation
- [ ] Short documentation of your parameter choices (sensor weights, speed values, reasoning)

!!! note "Assessment"
    This assignment is graded and counts towards the 70% in-semester component.

---

## Key Parameters to Tune

Your template controller will include adjustable parameters. Common values to experiment with:

| Parameter | Effect |
|---|---|
| Sensor weights | How strongly each sensor position influences steering |
| Base speed | Overall speed of the robot |
| Correction factor | How aggressively the robot steers to correct deviations |

Start with small corrections and increase gradually. A robot that overcorrects will oscillate rather than follow the line smoothly.

!!! tip "Extended variant"
    For the 8-sensor variant, think about how additional sensors near the centre vs. the edges help distinguish gradual curves from sharp turns. Colour variation requires adapting the threshold logic for surface detection.
