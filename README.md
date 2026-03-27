# lecture-auto

Accompanying material for the Master's course **Autonomous Logistics Systems and IoT** at the Digital Business Lab.

The course covers the use of Automated Guided Vehicles (AGVs) in intralogistics, with hands-on work in Webots, ROS/Gazebo, and Plant Simulation.

## Repository Structure

```
lecture-auto/
├── docs/                        # Concept and planning documents
│   ├── course-concept.md        # Full course concept (authoritative)
│   └── semester-prep.md         # Semester preparation checklist
├── block-01-foundations/        # Organisation & AGV fundamentals
├── block-02-webots/             # Classical AGVs — Webots simulation
│   ├── session-03.md            # Webots introduction
│   ├── session-04.md            # Labyrinth assignment
│   ├── session-06.md            # Sensor extension
│   └── session-07.md            # Line following
├── block-03-ros/                # Autonomous AGVs — ROS
│   ├── assignments/             # Guided activity sheets
│   └── scripts/                 # Pre-written ROS scripts
├── block-04-simulation/         # AGV Simulation — Plant Simulation
│   ├── assignments/             # Assignment sheet
│   └── models/                  # Plant Simulation model files
├── assessment/                  # Business case (primary assessment)
│   └── business-case/           # Template and grading rubric
└── web/                         # MkDocs source (docs_dir); deployed to GitHub Pages
   ├── block-01/                 # Block 1 content
   │   ├── agv-fundamentals.md
   │   ├── index.md
   │   ├── session-01.md
   │   └── session-02.md
   ├── block-02/                 # Block 2 content
   │   ├── index.md
   │   ├── session-03.md
   │   ├── session-04.md
   │   ├── session-06.md
   │   └── session-07.md
   ├── block-03/                 # Block 3 content
   │   ├── index.md
   │   ├── session-08.md
   │   └── session-09.md
   ├── block-04/                 # Block 4 content
   │   └── index.md
   └── assessment/               # Assessment content
      └── index.md
```

## Key Documents

| Document | Description |
|---|---|
| [`CLAUDE.md`](./CLAUDE.md) | Project memory: decisions, rationale, work packages — read first |
| [`docs/course-concept.md`](./docs/course-concept.md) | Full course concept: blocks, assignments, pedagogy, open questions |
| [`docs/semester-prep.md`](./docs/semester-prep.md) | Checklist for semester preparation (infrastructure, hardware, content) |

> Detailed content lives in `docs/` and the block folders. This file is a navigation hub only.