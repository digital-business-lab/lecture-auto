# Block 4 — AGV Simulation

Students simulate a shaft manufacturing scenario in two configurations (classical vs. AGV-supported) using **Plant Simulation (Siemens)**. They analyse throughput, lead times, and WIP, and draw business conclusions.

## Rationale

Students apply their accumulated understanding by analysing a complete manufacturing simulation. The contrast between classical and AGV-supported production layouts provides a concrete, evaluable scenario that connects technical content to business decision-making.

## Scenario — Shaft Manufacturing

Students work with a simulation of a production environment in two configurations:

1. **Classical layout** — manual transport between stations
2. **AGV-supported layout** — automated internal transport

Students build both models from scratch using Plant Simulation's GUI interface (no coding required), following step-by-step instructions. They then analyse throughput, lead times, WIP (work in progress), and bottlenecks, and draw conclusions about when and why AGV deployment creates value.

---

## Tool — Plant Simulation (Siemens) ✅ decided 2026-03-23

Institutional licences for Plant Simulation are available.

**Rationale:**
- GUI-based discrete event simulation — no programming required
- Industry-standard tool widely used in manufacturing and intralogistics
- Strong built-in support for material flow, conveyor systems, and AGV modelling
- Licence barrier removed (institutional access confirmed)

**Alternatives considered and not chosen:**

| Tool | Reason not chosen |
|---|---|
| AnyLogic | Also GUI-based and strong; rejected because Plant Simulation licences are already available, avoiding additional procurement and registration overhead |
| Webots | Already known to students but not suited for logistics process simulation and requires coding |
| Spreadsheet model | Too simplified for meaningful process analysis |

*Confirmed:* Plant Simulation runs natively on the lab computers (not in a VM).

---

## Assignment Overview

Students will:

1. **Build two Plant Simulation models from scratch** using the provided templates and step-by-step instructions
2. **Run simulations** for 480 minutes (8-hour shift) with multiple repetitions
3. **Collect and analyse data** on throughput, lead time, WIP, and bottlenecks
4. **Compare classical vs. AGV-supported layouts** using charts and statistical analysis
5. **Write a business report** with recommendations on whether AGV deployment creates value

---

## Open Questions

- Individual or group assignment?
- Presentation, written report, or both?

---

## Folder Structure

| Folder | Contents |
|---|---|
| `assignments/` | Assignment sheet with scenario description, tasks, and grading rubric |
| `models/` | Template files (`.spp`) with step-by-step building instructions and README guide |

## Status

| Item | Status |
|---|---|
| Assignment sheet | ✅ Done (AP8) |
| Building instructions for classical layout | ✅ Done (`models/README.md`) |
| Building instructions for AGV layout | ✅ Done (`models/README.md`) |
| Template files (placeholders) | ✅ Done (`classical_layout.spp`, `agv_supported_layout.spp`) |
