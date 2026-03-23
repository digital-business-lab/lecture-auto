# Session 4 — Labyrinth Assignment

**Duration: 3 hours · Graded**

---

## Goal

Implement a maze-solving strategy for a simulated AGV and present your results to the group.

---

## What You Receive

- A **pre-built labyrinth world** (`.wbt` file) — ready to open in Webots
- A **controller template** with `TODO` gaps marking the logic you need to implement

You never write code from scratch. Every non-trivial line is explained with inline comments.

---

## Your Task

1. Open the labyrinth world in Webots.
2. Study the controller template and understand the existing structure.
3. Complete the `TODO` sections — typically wall-following decision rules and direction logic.
4. Test your controller and refine the algorithm until the robot reliably exits the maze.
5. Prepare a short presentation of your approach.

---

## Deliverables

- [ ] A working Webots simulation in which your robot navigates the labyrinth
- [ ] A short in-session presentation of your approach and results (2–3 min)

!!! note "Assessment"
    This assignment is graded and counts towards the 70% in-semester component. Bring your completed simulation to the session.

---

## Hint — Wall Following

A common approach for maze-solving robots is the **wall-following algorithm**: the robot keeps one wall (left or right) consistently to its side and follows it until it exits. Think about:

- How does your robot detect walls? (distance sensors)
- When should it turn left, right, or go straight?
- What happens at dead ends?
