## PHYSICAL DESIGN

## SKY130 Module 1 - Inception of Open-Source EDA, OpenLANE and SKY130 PDK

### Introduction

This module introduces the fundamentals of digital ASIC design and the open-source EDA ecosystem. It explains how a digital circuit written in RTL is converted into a physical chip layout using the RTL-to-GDSII flow, OpenLANE, and the SKY130 PDK.

---

## SKY130_D1_SK1 - How to Talk to Computers

### Important Definitions

- **RTL:** Register Transfer Level. It describes the behavior of a digital circuit using Verilog or SystemVerilog.
- **Hardware Description Language:** A language used to describe the structure and behavior of digital circuits.
- **Simulation:** The process of verifying the functionality of an RTL design before synthesis.
- **Synthesis:** The process of converting RTL code into a gate-level netlist.
- **Netlist:** A representation of interconnected logic gates and standard cells.
- **PPA:** Power, Performance, and Area.
- **SoC:** System on Chip, which integrates processors, memory, controllers, and interfaces on a single chip.

### RTL-to-GDSII Flow

```text
RTL Design
    ↓
Functional Simulation
    ↓
Logic Synthesis
    ↓
Floorplanning
    ↓
Placement
    ↓
Clock Tree Synthesis
    ↓
Routing
    ↓
Physical Verification
    ↓
GDSII

```

## SKY130_D1_SK2 - SoC Design and OpenLANE

### What is an SoC?

An SoC, or System on Chip, combines multiple components such as processors, memory, controllers, and communication interfaces on a single integrated circuit.

### What is OpenLANE?

OpenLANE is an open-source automated RTL-to-GDSII design flow used for digital ASIC implementation. It performs synthesis, floorplanning, placement, clock tree synthesis, routing, and physical verification.

### What is SKY130 PDK?

The SKY130 PDK is an open-source Process Design Kit for SkyWater 130 nm technology. It provides the technology files, standard-cell libraries, design rules, timing information, and transistor models required for chip design.

### OpenLANE Design Flow

```text
RTL
 ↓
Yosys Synthesis
 ↓
Floorplanning
 ↓
Placement
 ↓
Clock Tree Synthesis
 ↓
Routing
 ↓
Magic and Netgen Verification
 ↓
GDSII
```

### Important Open-Source EDA Tools

| Tool | Purpose |
|---|---|
| Icarus Verilog | RTL simulation |
| GTKWave | Waveform viewing |
| Yosys | RTL synthesis |
| ABC | Logic optimization |
| OpenROAD | Physical design |
| OpenSTA | Static timing analysis |
| Magic | Layout and design-rule checking |
| Netgen | LVS verification |
| KLayout | Layout viewing |
| Verilator | RTL linting and simulation |

---

## SKY130_D1_SK3 - Get Familiar with Open-Source EDA Tools

### Required Tools

- Linux terminal
- Docker
- OpenLANE
- SKY130 PDK
- Yosys
- OpenROAD
- Magic
- Netgen
- GTKWave

### Check Linux Version

```bash
lsb_release -a
```



## Learning Outcomes

After completing Module 1, I understood:

- The basics of digital ASIC design
- The difference between RTL and a gate-level netlist
- The purpose of simulation and synthesis
- The importance of Power, Performance, and Area
- The complete RTL-to-GDSII flow
- The role of OpenLANE and the SKY130 PDK
- The purpose of open-source EDA tools
- How to use Linux and Docker for chip design
- How to run an OpenLANE design
- How to locate generated reports and floorplan files

## Conclusion

Module 1 provided a strong foundation in digital ASIC design and open-source EDA tools. It introduced the RTL-to-GDSII flow, OpenLANE, SKY130 PDK, Linux, Docker, and the tools used to convert RTL code into a physical chip layout.
# SKY130 Module 2 - Good Floorplanning

## Introduction

Floorplanning is one of the most important stages in the ASIC physical-design flow. It is the process of deciding the physical organization of a chip before the standard cells are placed and the connections are routed.

In this module, I learned how the die area and core area are defined, how the utilization factor and aspect ratio affect the design, and why the placement of macros, I/O pins, and power structures is important.

I also learned about library binding, standard-cell placement, cell characterization, and timing characteristics. The practical sessions helped me understand how OpenLANE performs floorplanning and how the generated layout and reports can be reviewed.

## ASIC Physical-Design Flow

The general physical-design flow is:

```text
RTL Design
    |
    v
Logic Synthesis
    |
    v
Floorplanning
    |
    v
Placement
    |
    v
Clock Tree Synthesis
    |
    v
Routing
    |
    v
Physical Verification
    |
    v
GDSII
```

Floorplanning provides the initial physical arrangement required for the later stages of placement, clock-tree synthesis, and routing.

<img src="./screenshots/floorplan_output.png" alt="Floorplan Output" width="800" height="500">



---

## SKY130_D2_SK1 - Floorplanning

### What is Floorplanning?

Floorplanning is the process of deciding the size and shape of the chip and arranging its major components inside the available area.

The main purpose of floorplanning is to create a physical structure that provides enough space for standard cells, macros, power connections, and signal routing.

A good floorplan should provide:

- Efficient area utilization
- Proper placement of macros
- Suitable I/O pin locations
- Reliable power distribution
- Reduced routing congestion
- Better timing performance
- Sufficient space for physical implementation

### Die Area

The **die area** is the complete physical area of the chip. It represents the outer boundary of the chip layout.

The die area contains:

- Core area
- I/O regions
- Power structures
- Standard cells
- Macros
- Routing resources

### Core Area

The **core area** is the region inside the die where the main logic cells and other functional blocks are placed.

The core area is smaller than the die area because space is required for I/O cells, power connections, and other physical structures.

### Utilization Factor

The utilization factor represents the percentage of the core area occupied by standard cells.

```text
Utilization Factor =
Area occupied by standard cells / Total core area × 100
```

For example, if standard cells occupy 60% of the core area, the utilization factor is 60%.

Very high utilization may cause routing congestion, while very low utilization may increase the chip area unnecessarily.

### Aspect Ratio

The aspect ratio is the ratio between the height and width of the core area.

```text
Aspect Ratio = Height / Width
```

An aspect ratio of 1 represents a square core. A suitable aspect ratio helps create an efficient and routable floorplan.

### Pre-Placed Cells

Pre-placed cells are cells or blocks that are positioned at fixed locations before the remaining standard cells are placed.

Examples include:

- Memory blocks
- Input/output cells
- Macros
- Special-purpose circuit blocks

Pre-placed cells help guide the placement process and ensure that important blocks are located correctly.

### De-Coupling Capacitors

De-coupling capacitors are used to reduce voltage fluctuations in the power supply.

They provide a temporary supply of current when the circuit experiences sudden changes in power demand. This helps maintain stable voltage levels and improves circuit reliability.

### Power Planning

Power planning involves creating the power-distribution network required to supply power to all the cells in the design.

It includes:

- Power rings
- Power stripes
- VDD connections
- VSS connections
- Power rails

Proper power planning reduces voltage drop and power-related reliability problems.

### Pin Placement and Logical Cell Placement

Pin placement is the process of deciding the locations of input and output pins around the chip boundary.

Proper pin placement helps to:

- Reduce wire length
- Avoid routing congestion
- Improve timing
- Simplify signal connections

Logical cell placement refers to arranging the standard cells inside the core area according to the design requirements.

### Steps to Run Floorplanning

The basic steps involved in running floorplanning are:

1. Read the design configuration.
2. Load the synthesized netlist.
3. Define the die area.
4. Define the core area.
5. Set the utilization factor.
6. Set the aspect ratio.
7. Place input and output pins.
8. Place pre-designed macros.
9. Create the power-distribution network.
10. Generate the initial floorplan.

### Review Floorplan Files and Reports

After floorplanning, different files and reports are generated for analysis.

These files help in checking:

- Die dimensions
- Core dimensions
- Cell placement
- Pin locations
- Utilization
- Power structures
- Routing resources

The reports are useful for identifying problems before moving to placement and routing.

### Review Floorplan Layout

The floorplan layout can be inspected using physical-design and layout-viewing tools.

During the review, the following points are checked:

- Whether the core area is properly defined
- Whether the cells are placed inside the core
- Whether the pins are correctly positioned
- Whether macros have sufficient spacing
- Whether power structures are properly connected
- Whether there is enough space for routing

![Floorplan Layout](screenshots/floorplan_layout.png)

---

## SKY130_D2_SK2 - Library Binding and Placement

This section explains how the synthesized design is connected to the standard-cell libraries and how the cells are placed inside the floorplan.

### What is Library Binding?

Library binding is the process of associating the logical cells in the synthesized netlist with the corresponding physical standard cells available in the technology library.

For example, a logical inverter in the netlist is mapped to a suitable inverter cell from the SKY130 standard-cell library.

Library binding provides the physical information required for placement and later stages of physical design.

### Netlist Binding and Initial Placement

Netlist binding connects the logical cells in the synthesized netlist with their corresponding physical standard cells.

Initial placement creates an approximate location for each standard cell inside the core area.

The objective is to obtain a placement that provides:

- Shorter connections
- Better timing
- Lower congestion
- Efficient area utilization

### Optimize Placement Using Timing Analysis

Placement optimization improves the locations of cells based on timing requirements.

Cells connected to critical paths may be placed closer together to reduce wire delay. The placement tool may also adjust cell positions to improve setup and hold timing.

### Final Placement Optimization

Final placement optimization makes the required adjustments before clock-tree synthesis and routing.

It focuses on:

- Reducing wire length
- Improving timing
- Reducing congestion
- Removing placement violations
- Improving overall design quality

### Need for Libraries and Characterization

Standard-cell libraries contain information about the electrical and physical properties of cells.

They provide:

- Cell functionality
- Cell dimensions
- Timing information
- Power information
- Input capacitance
- Output drive strength
- Physical layout data

Library characterization is necessary to understand how a cell behaves under different input, output, voltage, and load conditions.

### Congestion-Aware Placement

Congestion-aware placement tries to avoid placing too many cells in the same region.

High congestion can make routing difficult and may lead to:

- Longer wires
- Timing violations
- Routing failures
- Increased power consumption
- Design-rule violations

The placement tool distributes cells more effectively to provide sufficient routing space.

![Standard Cell Placement](screenshots/standard_cell_placement.png)

---

## SKY130_D2_SK3 - Cell Design and Characterization

This section introduces the process of designing and characterizing standard cells used in an ASIC.

### What is a Standard Cell?

A standard cell is a pre-designed and reusable logic block used in digital integrated circuits.

Examples include:

- Inverters
- AND gates
- OR gates
- NAND gates
- NOR gates
- Flip-flops
- Buffers
- Multiplexers

Standard cells have predefined physical dimensions, layouts, and electrical characteristics. They help reduce design time and make the physical-design process more efficient.

### Inputs for Cell Design Flow

The cell design flow requires several inputs, including:

- Circuit specifications
- Transistor models
- Technology information
- Design rules
- Power-supply requirements
- Timing requirements
- Cell functionality

These inputs are used to design a cell that satisfies the required electrical and physical specifications.

### Circuit Design Step

In the circuit-design stage, the transistor-level circuit is created according to the required logic function.

The design process includes:

1. Selecting suitable transistors
2. Creating the transistor-level schematic
3. Connecting the circuit components
4. Checking the logic functionality
5. Simulating the circuit
6. Verifying voltage and current behavior

### Layout Design Step

The layout-design stage converts the transistor-level circuit into a physical layout.

It includes:

- Drawing transistor geometries
- Creating metal connections
- Connecting power and ground
- Following design rules
- Checking the physical dimensions
- Preparing the layout for fabrication

### Typical Characterization Flow

Cell characterization determines the timing and power behavior of a standard cell.

The typical flow includes:

1. Design the transistor-level circuit.
2. Create the physical layout.
3. Verify the layout using design-rule checks.
4. Extract parasitic information.
5. Run electrical simulations.
6. Measure timing and power values.
7. Generate the standard-cell library models.

The characterized data is later used by synthesis, placement, timing analysis, and routing tools.



## SKY130_D2_SK4 - General Timing Characteristics

This section introduces the basic timing concepts used to analyze the performance of digital circuits.

### What are Timing Characteristics?

Timing characteristics describe how quickly a standard cell responds to an input signal and produces an output signal.

They are important because the delay of individual cells and interconnections affects the overall operating speed of a chip.

### Timing Threshold Definitions

Timing measurements are taken at specific voltage thresholds.

Common timing thresholds are used to identify:

- Input transition time
- Output transition time
- Propagation delay
- Rise time
- Fall time

These thresholds provide a consistent method for measuring the timing behavior of a cell.

### Propagation Delay

Propagation delay is the time taken for a change at the input of a cell to produce a corresponding change at its output.

```text
Propagation Delay = Output response time - Input transition time
```

A smaller propagation delay generally allows the circuit to operate at a higher speed.

### Transition Time

Transition time is the time required for a signal to change from one voltage level to another.

The two main types of transition time are:

- **Rise time:** The time taken for a signal to change from a low voltage level to a high voltage level.
- **Fall time:** The time taken for a signal to change from a high voltage level to a low voltage level.

Good timing characteristics are important for achieving high-speed and reliable circuit operation.

### Importance of Timing Analysis

Timing analysis helps to identify:

- Critical paths
- Setup-time violations
- Hold-time violations
- Excessive cell delay
- Long interconnection delays
- Maximum operating frequency

![Timing Waveform](screenshots/timing_waveform.png)

---

## Important Commands Used in Floorplanning

### Enter the OpenLANE Container

Run the following command in the normal Ubuntu terminal:

```bash
docker run -it \
-v /mnt/openlane/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane:/openLANE_flow \
-v /mnt/openlane/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks:/pdks \
-e PDK_ROOT=/pdks \
-e PDK=sky130A \
-e STD_CELL_LIBRARY=sky130_fd_sc_hd \
-u $(id -u):$(id -g) \
ghcr.io/the-openroad-project/openlane:ff5509f65b17bfa4068d5336495ab1718987ff69
```

This command starts the OpenLANE Docker container and connects the OpenLANE flow and SKY130 PDK directories.

### Navigate to the OpenLANE Directory

```bash
cd /openLANE_flow
```

This command moves to the OpenLANE working directory.

### Run the Floorplanning Flow

```bash
flow.tcl -design /openLANE_flow/designs/picorv32a -ignore_mismatches
```

This command starts the OpenLANE flow for the `picorv32a` design.

### View the Design Configuration

```bash
cat /openLANE_flow/designs/picorv32a/config.tcl
```

This command displays the design configuration file.

The configuration file contains information such as:

- Design name
- Verilog source files
- SDC file
- Clock period
- Clock port
- Technology settings

### List Available Run Directories

```bash
ls /openLANE_flow/designs/picorv32a/runs
```

This command lists the available OpenLANE run directories.

### Search for Floorplan Files

```bash
find /openLANE_flow/designs/picorv32a/runs -type f | grep floorplan
```

This command searches for files related to the floorplanning stage.

### Check Disk Space

```bash
df -h
```

This command displays the available disk space and helps identify storage problems during the OpenLANE flow.

### Check PDK Storage Usage

```bash
du -sh /pdks/*
```

This command shows how much storage is occupied by the PDK directories.

### View the Layout Using Magic

```bash
magic -T sky130A.tech
```

This command opens Magic for viewing and inspecting the physical layout.

> **Note:** Use the exact commands and paths provided by your instructor or workshop environment. The design name and directory paths may differ between installations.

---

## Practical Workflow

The practical workflow followed in this module is:

```text
Start Ubuntu
     |
     v
Open Docker Container
     |
     v
Navigate to OpenLANE Directory
     |
     v
Select the Design
     |
     v
Run OpenLANE Flow
     |
     v
Generate Floorplan
     |
     v
Review Reports and Files
     |
     v
Inspect Layout
     |
     v
Analyze Placement and Timing
```


> Replace the placeholder image paths with the actual screenshot filenames uploaded to the `screenshots` folder in your GitHub repository.

## Overall Learning Outcome

Through this module, I understood the importance of floorplanning in the ASIC physical-design flow. I learned how the die area, core area, utilization factor, aspect ratio, pre-placed cells, de-coupling capacitors, power planning, and pin placement affect the physical implementation of a chip.

I also learned how library binding connects logical cells with physical standard cells, how placement optimization reduces timing problems and congestion, and how standard-cell characterization provides timing and power information.

The practical sessions helped me understand how to run the OpenLANE floorplanning flow, inspect the generated reports, review the layout, and analyze the physical design before moving to the next stages.

## Key Takeaways

- Floorplanning determines the physical organization of a chip.
- Utilization and aspect ratio affect area and routability.
- Pre-placed cells and macros must be positioned carefully.
- De-coupling capacitors help maintain stable power supply voltage.
- Power planning provides reliable power to the complete design.
- Proper pin placement reduces routing complexity.
- Library binding connects logical cells with physical standard cells.
- Placement optimization improves timing and reduces congestion.
- Standard-cell characterization provides timing and power information.
- Propagation delay and transition time are important timing parameters.
- OpenLANE automates the floorplanning process using open-source EDA tools.
