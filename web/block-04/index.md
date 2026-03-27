# Block 4 — AGV Simulation

**Sessions 10–12 · Duration: approx. 3 weeks**

## Assignment Overview

In this assignment, you will build and analyze an **AGV-supported production line** using **Plant Simulation (Siemens)**. You will create a simulation model from scratch, then run multiple scenarios with different parameters to understand how AGV deployment affects production performance.

Your task is to build the model, run simulations with varying parameters, collect performance data, and draw business conclusions about optimal AGV deployment.

## Getting Started with Plant Simulation

### Installation & Access

Plant Simulation is pre-installed on all lab computers. If you need to access it:

1. Log into a lab computer
2. Launch Plant Simulation from the Start Menu or Applications folder
3. If prompted, enter your institutional credentials

### Creating Your First Model

1. **Start a new model:**
   - Open Plant Simulation
   - Click `File` → `New Model` or press `Ctrl+N`

2. **Save your model:**
   - Click `File` → `Save As` or press `Ctrl+S`
   - Save to this directory: `block-04-simulation/models/`
   - Name it: `agv_supported_layout.spp`

3. **Save frequently** — Plant Simulation can crash unexpectedly during development.

## Building the AGV-Supported Layout Model

This section provides a step-by-step guide to creating the AGV-supported production line model in Plant Simulation:

1. **Add Raw Material Source**
   - Drag a `Source` object from the Library to the simulation canvas
   - Name it: `RawMaterialStorage`
   - Configure its properties:
     - Generate rate: Random interval between 5–10 minutes (`randomUniform(5, 10)`)
     - Product type: Shaft

2. **Add Station Buffers**
   - For each station, add a `Table` object to serve as input/output buffer
   - Name them: `CNC_Buffer`, `Quality_Buffer`, `Packaging_Buffer`

3. **Add Processing Stations**
   - Drag three `Machine` objects from the Library
   - Name them: `CNC_Machining`, `QualityInspection`, `Packaging`
   - Configure processing times:
     - CNC_Machining: Random between 8–12 minutes (`randomUniform(8, 12)`)
     - QualityInspection: Random between 3–5 minutes (`randomUniform(3, 5)`)
     - Packaging: Random between 2–4 minutes (`randomUniform(2, 4)`)

4. **Add Finished Goods Sink**
   - Drag a `Sink` object from the Library
   - Name it: `FinishedGoodsStorage`

5. **Connect Buffers to Machines**
   - Use the **Connector** tool from the toolbar (or press `C`)
   - Connect each buffer to its corresponding machine:
     - CNC_Buffer → CNC_Machining (transport time = 0)
     - Quality_Buffer → QualityInspection (transport time = 0)
     - Packaging_Buffer → Packaging (transport time = 0)

6. **Add AGV Transport System**
   - Navigate to `Logistics` → `Transporter` in the Library
   - Drag a Transporter object onto the canvas
   - Rename it: `AGV_System`
   - Configure AGV properties:
     - Set **Speed** → `20` (m/min)
     - Set **Number of AGVs** → Start with 1, then experiment with 2 and 3
     - Enable **Automatic Loading/Unloading**

7. **Define Transport Routes**
   - Navigate to `Logistics` → `Path` in the Library
   - Drag Path objects onto the canvas to create routes:
     - RawMaterialStorage → CNC_Buffer (via AGV)
     - CNC_Machining → Quality_Buffer (via AGV)
     - QualityInspection → Packaging_Buffer (via AGV)
   - Configure each Path:
     - Set **Transport Time** → `Random` → `randomUniform(1, 3)` minutes
     - This simulates AGV travel time between stations

8. **Connect Everything to AGV System**
   - Use the **Connector** tool
   - Connect each station's output to the next station's buffer via AGV:
     - RawMaterialStorage → CNC_Buffer (via AGV)
     - CNC_Machining → Quality_Buffer (via AGV)
     - QualityInspection → Packaging_Buffer (via AGV)

9. **Connect Final Output**
   - Use the **Connector** tool
   - Connect Packaging → FinishedGoodsStorage (transport time = 0)

10. **Configure Simulation Parameters**
    - Click on the **Simulation** menu
    - Set **Duration** → `480` (minutes, representing an 8-hour shift)
    - Enable statistics collection for all objects

11. **Run and Validate**
    - Click the **Run** button (green play icon)
    - Watch products flow through the system via AGVs
    - Check that all statistics are being collected

## Running Multiple Scenarios

After building your model, you will run it with different scenarios:

### Scenario 1: Single AGV
- Set **Number of AGVs** → `1`
- Run simulation 5 times with different random seeds
- Collect data: throughput, lead time, WIP levels

### Scenario 2: Two AGVs (Baseline)
- Set **Number of AGVs** → `2`
- Run simulation 5 times with different random seeds
- Collect data: throughput, lead time, WIP levels

### Scenario 3: Three AGVs
- Set **Number of AGVs** → `3`
- Run simulation 5 times with different random seeds
- Collect data: throughput, lead time, WIP levels

### Scenario 4: High Transport Times
- Set **Number of AGVs** → `2`
- Change transport times to: `randomUniform(3, 5)` minutes
- Run simulation 5 times with different random seeds
- Collect data: throughput, lead time, WIP levels

## Collecting Results

### Viewing Statistics

1. Right-click any object → **Properties** → **Statistics**
2. View key metrics:
   - **Throughput**: Number of products processed per hour
   - **Utilisation**: Percentage of time the object is busy
   - **Queue Length**: Average number of items waiting

### Creating Charts

1. Click `Tools` → **Chart**
2. Select the data you want to visualize:
   - Throughput over time
   - Queue lengths at each station
   - Machine utilisation rates

### Exporting Data

1. Right-click any object → **Export** → `Table`
2. Save as CSV for analysis in Excel or other tools

## Expected Results (for validation)

| Scenario | AGV Count | Transport Time | Expected Throughput | Notes |
|---|---|---|---|---|
| 1 | 1 | 1–3 min | ~20-30 units/hr | Likely bottlenecked by single AGV |
| 2 | 2 | 1–3 min | ~30-45 units/hr | Baseline configuration |
| 3 | 3 | 1–3 min | ~35-50 units/hr | Diminishing returns expected |
| 4 | 2 | 3–5 min | ~15-30 units/hr | High transport times create bottleneck |

## Troubleshooting

### Simulation Won't Run

- Check that all objects are properly connected
- Verify no circular dependencies exist
- Ensure simulation duration is set correctly

### Products Getting Stuck

- Check buffer capacities (default is usually 10)
- Increase buffer sizes if needed
- Verify transport times aren't too long

### AGVs Not Moving

- Ensure paths are properly defined
- Check that AGV speed is set > 0
- Verify number of AGVs is at least 1

### Statistics Not Collecting

- Enable statistics in object properties
- Run simulation for full duration before checking results

## Tasks

### Task 1: Build the AGV Simulation Model (40%)

You will create a Plant Simulation model from scratch representing an AGV-supported production line. Follow the steps in the "Building the AGV-Supported Layout Model" section to construct your simulation model. Then configure the following additional parameters:

- Set simulation duration: **480 minutes** (8-hour shift)
- Enable statistics collection for all objects
- Run the simulation and verify that products flow through all stations correctly

### Task 2: Run Multiple Scenarios (30%)

Now you will run the simulation with different scenarios to understand how AGV parameters affect production performance.

#### Scenario 1: Single AGV
- Configure the model with **1 AGV**
- Run simulation 5 times (use different random seeds)
- Collect data for: throughput, lead time, WIP levels

#### Scenario 2: Two AGVs (Baseline)
- Configure the model with **2 AGVs**
- Run simulation 5 times (use different random seeds)
- Collect data for: throughput, lead time, WIP levels

#### Scenario 3: Three AGVs
- Configure the model with **3 AGVs**
- Run simulation 5 times (use different random seeds)
- Collect data for: throughput, lead time, WIP levels

#### Scenario 4: High Transport Times
- Configure the model with **2 AGVs** but increase transport times to 3–5 minutes
- Run simulation 5 times (use different random seeds)
- Collect data for: throughput, lead time, WIP levels

### Task 3: Comparative Analysis (15%)

Analyze your simulation results and create visualizations:

1. **Throughput Comparison**
   - Create a chart showing average throughput per hour for each scenario
   - Identify which AGV count provides optimal throughput

2. **Lead Time Distribution**
   - Create a chart showing average lead time for each scenario
   - Note how transport times affect overall production speed

3. **WIP Levels**
   - Create a chart showing maximum WIP at each station for each scenario
   - Identify where bottleneques form

4. **Utilization Analysis**
   - Calculate machine utilization percentages for each scenario
   - Identify which machines are bottlenecks

### Task 4: Business Recommendations (15%)

Based on your analysis, prepare a short report addressing the following questions:

1. **Optimal AGV Count**
   - How many AGVs should the company deploy?
   - What is the trade-off between additional AGV cost and throughput gains?

2. **When Does AGV Deployment Create Value?**
   - Under what production volumes or constraints?
   - What minimum throughput justifies the investment?

3. **What Are the Trade-offs?**
   - Consider capital investment, operational flexibility, and maintenance
   - What happens when transport times increase (e.g., due to congestion)?

4. **Recommendation for the Company**
   - Should they adopt AGVs? Why or why not?
   - What conditions would make the investment worthwhile?

## Deliverables

Submit the following:

1. **Simulation Model File** (`.spp`)
   - Your completed Plant Simulation model (`agv_supported_layout.spp`)

2. **Simulation Results Document** (PDF)
   - Tables with collected data from all runs
   - Charts and visualizations showing scenario comparisons
   - Brief interpretation of results

3. **Business Report** (PDF, max 3 pages)
   - Comparative analysis of all scenarios
   - Your recommendations with justification

## Grading Rubric

| Criterion | Excellent (90–100%) | Good (75–89%) | Satisfactory (60–74%) | Needs Improvement (<60%) |
|---|---|---|---|---|
| **Model Building** | All components correctly configured; model runs without errors | Most components correct; minor issues | Some configuration errors; model has problems | Major setup issues; model doesn't run properly |
| **Scenario Execution** | All 4 scenarios completed with 5+ runs each; data collected comprehensively | Most scenarios completed adequately | Some scenarios missing or incomplete | Incomplete scenario execution |
| **Data Analysis** | Clear, accurate tables and charts; thorough bottleneck identification | Good visualisations; identifies main bottlenecks | Basic analysis; some missing insights | Incomplete or inaccurate analysis |
| **Business Recommendations** | Well-reasoned, data-driven recommendations with clear justification | Solid recommendations supported by analysis | Basic recommendations; weak justification | Unclear or unsupported conclusions |
| **Report Quality** | Professional presentation; clear writing; proper formatting | Good structure and readability | Acceptable quality; minor issues | Poor organisation or presentation |

## Submission Deadline

**[Insert deadline date]**

Submit your deliverables via [insert submission method: Moodle/Email/GitHub].

## Tips for Success

- Start early to allow time for multiple simulation runs
- Use Plant Simulation's built-in analysis tools (e.g., Table, Chart)
- Document your methodology for reproducibility
- Focus on the business implications of technical results
- Experiment with different AGV counts to find optimal configuration

## Resources

- Plant Simulation User Guide (available via institutional licence)
- Lecture slides on discrete event simulation and AGV systems
- Office hours: [insert schedule]

*This assignment is designed to be completed without programming experience. All necessary tools are provided via Plant Simulation's GUI interface.*