# CLAUDE.md

> Read this before starting any work. Keep it lean — deep context lives in `docs/`.
> **Size limit: max 5,000 tokens.** If edits would exceed this, trim or move content to `docs/` first.

## Project

Master's course on AGV use in intralogistics. Repo: [`digital-business-lab/lecture-auto`](https://github.com/digital-business-lab/lecture-auto) (public).
**Target group: BWL Master's students — no programming background.**

## Repository Layout

```
docs/                    # course-concept.md (authoritative), semester-prep.md
block-01-foundations/
block-02-webots/         # assignments/, templates/ (TODO-gap files), worlds/
block-03-ros/            # assignments/, scripts/ (pre-written, students don't author)
block-04-simulation/     # assignments/, models/ (Plant Simulation)
assessment/business-case/
web/                     # MkDocs source (docs_dir); deployed to GitHub Pages
.github/workflows/       # deploy-mkdocs.yml → Actions-based Pages deployment
```

## Key Conventions

- **Language:** Repo files and all content in English. Communication with lecturer in German.
- **README.md:** Navigation hub only. Never put detailed content there.
- **Copyright:** Only self-authored material in the repo. Slides with third-party images → Moodle only.
- **Commits:** English, conventional commits (`feat:`, `fix:`, `docs:`, `ci:`), one logical change per commit.
- **Branches:** Feature branches for larger work; direct commits to `main` for docs.

## Build & Deploy

```bash
# Local preview
pip install mkdocs-material
mkdocs serve

# Deployment: automatic on push to main via GitHub Actions
# GitHub Pages source must be set to "GitHub Actions" in repo Settings → Pages
```

## Design Decisions (what & why)

| Decision | Rationale |
|---|---|
| Template-based coding ("Light Coding") for all Webots assignments | No programming background — students fill TODO gaps, never write from scratch |
| ROS block: demo-first, pre-written scripts, no from-scratch coding | From-scratch ROS nodes are infeasible without Python knowledge |
| Block 4 tool: Plant Simulation (Siemens) | Institutional licences available; GUI-based, no coding required |
| Assessment: 70% in-semester (Blocks 2–4) + 30% business case (semester break) | Business case suits BWL competencies; internal 70% weighting deferred (→ Q4a) |
| Labyrinth world provided pre-built | Students focus on algorithm, not environment modelling |
| MkDocs + GitHub Pages for self-study content | Self-authored only; public access without login or access management |
| Slides distributed via Moodle only | Contain third-party images that cannot be published |

## Open Work Packages

| ID | Task |
|---|---|
| AP2 | Webots intro tutorial (VM setup, first robot, first controller) |
| AP3 | Labyrinth assignment (pre-built world + code template) |
| AP4 | Line-following tutorial (basic 4-sensor + extended 8-sensor) |
| AP5 | ROS activity: fundamentals + running provided scripts |
| AP6 | ROS activity: SLAM & navigation in Gazebo (pre-configured) |
| AP7 | ROS activity: modify a provided node (no from-scratch coding) |
| AP8 | Plant Simulation assignment: shaft manufacturing scenario |
| AP9 | Business case template + grading rubric |
| AP10 | Finalise concept; align with semester schedule |

## Known Gotchas

- VM specs not yet confirmed — verify Webots and Gazebo/ROS run before semester starts (→ `docs/semester-prep.md`).
- Plant Simulation runs natively on lab computers (not in a VM).
- Internal weighting of the 70% in-semester grade is deferred until AP3, AP5, AP8 are scoped (Q4a).
