# AGV Fundamentals

This page summarises the theoretical content from Block 1 for self-study and revision.

---

## Definition

An **Automated Guided Vehicle (AGV)** — in German: *Fahrerloses Transportsystem (FTS)* — is defined by VDI guideline 2510 as:

> An in-plant, floor-bound conveying system with automatically controlled vehicles, whose primary task is material transport — not the transport of persons.

Key characteristics:

- Operates **within a facility** (intralogistics, not public roads)
- **Floor-bound** movement (no aerial or rail systems)
- **Automatically controlled** — no human driver
- Designed for **material transport**

---

## Four Epochs of AGV Development

| Epoch | Period | Characteristic |
|---|---|---|
| 1 | ~1955–1975 | Idea and early implementation; first inductively guided vehicles |
| 2 | ~1975–1995 | Automation euphoria; rapid adoption in manufacturing |
| 3 | ~1995–2010 | Established technology for intralogistics; standardisation |
| 4 | ~2010–today | Classical AGVs plus innovative autonomous systems (AMRs) |

---

## Core Technical Components

### 1. Navigation & Guidance
How the vehicle knows where it is and where to go.

| Method | Principle | Typical use |
|---|---|---|
| **Inductive** | Wire embedded in floor carries current; vehicle follows magnetic field | Fixed routes, heavy industry |
| **Optical** | Vehicle follows a painted or taped line on the floor | Simple, low-cost installations |
| **Laser (reflector-based)** | Laser scanner measures distance to fixed reflectors | Flexible, reprogrammable routes |
| **Natural navigation** | SLAM — vehicle builds a map of its environment using sensors | Modern AMRs; no infrastructure needed |
| **Magnetic spots** | Grid of magnets in floor; vehicle navigates by counting spots | High precision in confined areas |

### 2. Safety Systems

AGVs share space with people and must meet strict safety standards (EN ISO 3691-4).

- **Laser scanners** (protective field): detect obstacles and trigger emergency stop
- **Bumpers**: mechanical contact detection as a last resort
- **Warning lights and sound signals**: alert people to the vehicle's presence and intentions
- **Speed reduction**: vehicle slows in monitored zones, stops in protective zones

### 3. Fleet Management (Leitsteuerung)

The fleet management system coordinates multiple AGVs:

- Assigns transport orders to available vehicles
- Manages traffic (collision avoidance, intersection control)
- Monitors battery status and dispatches vehicles for charging
- Interfaces with warehouse management systems (WMS) and ERP

### 4. Vehicle Types

| Type | Load handling | Typical application |
|---|---|---|
| **Towing vehicle** | Tows trailers | Long-distance transport in large facilities |
| **Unit load carrier** | Carries pallets, containers | Warehouse and production |
| **Fork AGV** | Forks load from floor or rack | High-bay warehouses |
| **Underride vehicle** | Slides under load carrier, lifts it | E-commerce fulfilment |
| **Assembly AGV** | Carries product through assembly line | Automotive manufacturing |

### 5. Operating Environment

AGVs require a prepared environment:

- **Floor quality:** smooth, level, sufficient load-bearing capacity
- **Navigation infrastructure:** reflectors, markers, or mapped environment (depending on navigation type)
- **Traffic zones:** clearly defined routes, intersections, waiting areas
- **Charging stations:** opportunity charging (brief top-ups) or full charging bays

### 6. Trends and Future Developments

- **Autonomous Mobile Robots (AMRs):** natural navigation, dynamic obstacle avoidance, no fixed infrastructure
- **Collaborative operation:** AGVs and humans working in shared spaces (cobots)
- **AI-based fleet optimisation:** dynamic order prioritisation, predictive maintenance
- **Swarm intelligence:** decentralised coordination without central controller
- **Integration with IoT:** real-time data from vehicles fed into digital twin, WMS, ERP

---

## Key Distinction: Classical AGV vs. AMR

| | Classical AGV | AMR (Autonomous Mobile Robot) |
|---|---|---|
| Navigation | Fixed infrastructure (wire, tape, reflectors) | Natural navigation (SLAM) |
| Route changes | Requires physical changes to facility | Software update only |
| Obstacle handling | Emergency stop | Dynamic re-routing |
| Cost | Higher upfront (infrastructure) | Higher unit cost, lower installation cost |
| Flexibility | Low | High |

!!! tip "Exam relevance"
    The AGV vs. AMR distinction frequently appears in business case analyses. Understanding when to choose which system is directly relevant to the course assessment.
