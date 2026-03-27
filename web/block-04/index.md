# Block 4 — AGV Simulation

**Sessions 10–12 · Duration: approx. 3 weeks**

## Assignment Overview

In this assignment, you will build and analyze an **AGV-supported production line** using **Plant Simulation (Siemens)**. You will create a simulation model from scratch, then run multiple scenarios with different parameters to understand how AGV deployment affects production performance.

Your task is to build the model, run simulations with varying parameters, collect performance data, and draw business conclusions about optimal AGV deployment.

## Getting Started with Plant Simulation

For detailed instructions on setting up and using Plant Simulation, please refer to the [Getting Started guide](getting-started.md).



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