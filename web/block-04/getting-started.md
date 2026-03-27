# Getting Started with Plant Simulation

## Installation & Access

Plant Simulation is pre-installed on all lab computers. If you need to access it:

1. Log into a lab computer
2. Launch Plant Simulation from the Start Menu or Applications folder
3. If prompted, enter your institutional credentials

## Creating Your First Model

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
