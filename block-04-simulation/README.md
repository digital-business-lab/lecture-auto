# Block 4 — AGV Simulation

Students simulate a shaft manufacturing scenario in two configurations (classical vs. AGV-supported) using **Plant Simulation (Siemens)**. They analyse throughput, lead times, and WIP, and draw business conclusions.

## Rationale

Students apply their accumulated understanding by analysing a complete manufacturing simulation. The contrast between classical and AGV-supported production layouts provides a concrete, evaluable scenario that connects technical content to business decision-making.

## Scenario — Shaft Manufacturing

Students work with a simulation of a production environment in two configurations:

1. **Classical layout** — manual transport between stations
2. **AGV-supported layout** — automated internal transport

They analyse throughput, lead times, WIP (work in progress), and bottlenecks, and draw conclusions about when and why AGV deployment creates value.

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

## Open Questions

- Individual or group assignment?
- Presentation, written report, or both?

---

## Folder Structure

| Folder | Contents |
|---|---|
| `assignments/` | Assignment sheet with scenario description, tasks, and grading rubric |
| `models/` | Plant Simulation model files (`.spp`) provided to students |

## Status

| Item | Status |
|---|---|
| Assignment sheet | ⏳ To do (AP8) |
| Plant Simulation model — classical layout | ⏳ To do (AP8) |
| Plant Simulation model — AGV layout | ⏳ To do (AP8) |
