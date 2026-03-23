# Block 1 — Detailed Session Plan

> **Audience:** Lecturer reference. Not published on the course website.
> **Format:** Two sessions of approx. 3 hours each. Lecture + group work + short presentations.

---

## Session 1 — Organisation & AGV Foundations

**Duration:** 3 h · **Method:** Lecturer input, group work, plenary presentations

### Agenda

| # | Topic | Method | Material |
|---|---|---|---|
| 1 | **Organisation** — course structure, schedule, assessment, tools & infrastructure | Lecturer input | Slides: course map, assessment overview, tool overview |
| 2 | **AGV epochs** — four phases of AGV/FTS development | Group work + short presentations | Assignment sheet: one epoch per group; timeline reference |
| 3 | **Task-related aspects of AGV deployment** — which transport tasks suit AGVs? (load types, flow regularity, throughput, cycle times) | Lecturer input | Slides with examples |
| 4 | **Deployment modes** — unit load carrier, towing, fork AGV, underride, assembly line | Lecturer input | Slides with photos |
| 5 | **Alternatives to AGVs** — conveyor systems, forklifts, AMRs, manual transport | Lecturer input | Slides: comparison overview |
| 6 | **Suitability of alternatives** — which solution fits which scenario? | Group work + short presentations | Scenario cards (one scenario per group) |

### Group Work Details

**Topic 2 — AGV epochs:**
- Groups of 2–3 students; one epoch per group
- Epochs: (1) wire-guided early systems, (2) laser/optical guidance era, (3) natural navigation & fleet management, (4) AMR and AI-based systems
- Task: summarise key characteristics and give one concrete example
- Presentation: 2–3 min per group

**Topic 6 — Suitability of alternatives (two-step structure):**

*Step 1 — Lecturer input (whole class):*
Before the group work, the lecturer presents a pre-filled comparison table of all five alternatives across the five criteria. This gives every group the same reference knowledge and avoids each group having to research generic properties independently.

Reference table (shown on slide and printed on scenario card):

| Alternative | Flexibility | Investment cost | Personnel requirement | Throughput capacity | Infrastructure effort |
|---|---|---|---|---|---|
| Manual transport | High | Low | High | Low | None |
| Forklift | High | Low–Medium | Medium | Medium | Low |
| Conveyor system | Low | High | Low | High | High |
| AGV | Low–Medium | High | Low | High | High |
| AMR | High | High | Low | Medium | Low |

Criteria definitions (on slide and printed on scenario card):
- **Flexibility** — ease of adapting routes or layout without major cost
- **Investment cost** — upfront capital expenditure
- **Personnel requirement** — ongoing need for human operators
- **Throughput capacity** — volume of transport tasks the system can handle
- **Infrastructure effort** — floor preparation, IT integration, facility changes required

*Step 2 — Group work:*
- Groups receive a scenario card with a concrete logistics situation; one scenario per group
- Task: work through each criterion and explain how it plays out in their specific scenario — then derive a recommendation
- Output template (printed on the scenario card):

| Criterion | How does it apply to our scenario? | Implication for the choice |
|---|---|---|
| Flexibility | | |
| Investment cost | | |
| Personnel requirement | | |
| Throughput capacity | | |
| Infrastructure effort | | |

**Our recommendation:** *(alternative)* — because *(2–3 sentences)*

- Presentation: 2–3 min per group — walk through two or three criteria and state the recommendation

**Scenario cards (one per group):**

| Card | Scenario |
|---|---|
| A | *Pharmaceutical production:* clean-room environment, strict documentation requirements, 200 transport orders/day, stable routes, high regulatory compliance demands |
| B | *E-commerce fulfilment:* high SKU variety, strongly seasonal volume peaks (3× normal at peak), frequent layout changes due to product range shifts |
| C | *Automotive body shop:* heavy loads (up to 2 t), fixed assembly line sequence, continuous 3-shift operation, high throughput, very stable routes |
| D | *Hospital logistics:* mixed-use corridors shared with people, variable demand across wards, sterile goods and linen, strict hygiene requirements |
| E | *Food & beverage warehouse:* cold-storage environment (−22 °C), pallet-level transport, medium throughput, strict traceability requirements |

**Lecturer note:** There is no single correct answer. Debrief by asking groups what they would change if one parameter shifted (e.g. "what if throughput doubled?" or "what if the building layout changes every six months?"). This previews the sensitivity analysis logic used later in the business case.

**Connection to assessment:** The two-step structure — first establish general properties, then apply them to a concrete situation — is the same logic used in the Nutzwertanalyse in the business case. Name this connection explicitly in the debrief.

### Preparation Checklist
- [ ] Slides for organisational part (course map, assessment, tools)
- [ ] Epoch assignment cards (4 cards, one per group)
- [ ] Scenario cards for suitability exercise (Cards A–E, see group work details above); print one per group, include decision matrix and criteria definitions
- [ ] Timeline graphic for AGV epochs
- [ ] Short video clip of an AGV system in operation (2–3 min, warm-up or intro)

### Notes
- Keep the organisational part focused — students do not need every detail in session 1; point them to Moodle for the rest.
- The epoch group work doubles as a first icebreaker; keep groups small and time-box strictly.
- The suitability exercise builds on the immediately preceding lecturer content — sequence matters.

---

## Session 2 — AGV Technology

**Duration:** 3 h · **Method:** Group work, lecturer input

### Agenda

| # | Topic | Method | Material |
|---|---|---|---|
| 1 | **Industry-specific aspects and examples** — AGV applications across sectors (automotive, e-commerce, healthcare, food, pharma) | Group work + plenary discussion | Research cards or short reading materials per sector |
| 2 | **Technology of the overall system** — navigation & guidance, fleet management, safety, infrastructure, WMS/ERP integration | Lecturer input | Slides with diagrams |
| 3 | **Technology of the transport vehicles** — vehicle types in detail, load handling, energy supply, sensor systems | Lecturer input | Slides with photos and technical sketches |

### Group Work Details

**Topic 1 — Industry-specific aspects:**
- Groups of 2–3 students; one sector per group
- Task: identify the specific requirements of the sector (load types, environment, cycle times, regulatory constraints) and describe one concrete AGV application
- Plenary: brief report-back (2–3 min per group) + lecturer comment
- Note: this can re-use groups from session 1 or be reassigned

### Technology Deep-Dive Breakdown (Topics 2 & 3)

| Sub-topic | Key points |
|---|---|
| Navigation & guidance | Inductive, optical, laser (reflector), natural (SLAM), magnetic spots |
| Fleet management | Order assignment, traffic control, charging management, WMS/ERP interface |
| Safety | EN ISO 3691-4, laser scanners, bumpers, warning signals, speed zones |
| Infrastructure | Floor requirements, traffic zones, charging bays, route planning |
| Vehicle types | Towing AGV, unit load carrier, fork AGV, underride AGV, assembly AGV |
| Load handling | Roller conveyors, lift platforms, fork mechanisms, custom interfaces |
| Energy supply | Opportunity charging, inductive charging, battery swap |
| Sensor systems | Laser scanners, ultrasonic, cameras, encoders |

### Preparation Checklist
- [ ] Sector research cards (automotive, e-commerce, healthcare, food, pharma — one per group)
- [ ] Slides for overall system technology
- [ ] Slides for vehicle technology (photos, technical drawings)
- [ ] AGV vs. AMR comparison (brief — builds on Session 1 content)

### Notes
- The industry group work at the start of session 2 connects back to the suitability exercise from session 1 — draw this link explicitly.
- Use analogies throughout the technology sections: "fleet management like air traffic control", "laser scanner like a rotating flashlight".
- Students have no technical background — focus on function and business relevance, not engineering detail.
- Flag the AGV vs. AMR distinction as relevant for the assessment.

---

*Updated 2026-03-23. Lecturer reference only.*
