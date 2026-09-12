# Sky130 Module 1 – Inception of Open-Source EDA, OpenLANE and Sky130 PDK

This module focuses on the fundamentals of **digital ASIC design, processor architecture, open-source EDA tools, and the complete RTL-to-GDSII flow** used to convert a digital design into a physical chip layout.

## RISC-V Architecture

**RISC-V** is an open and royalty-free **Instruction Set Architecture (ISA)** based on the Reduced Instruction Set Computer (RISC) concept.

An ISA defines the instructions that a processor can understand and execute, including:

- Arithmetic operations
- Logical operations
- Memory-access operations
- Control-flow operations

RISC-V follows a **modular architecture**, allowing designers to add different instruction-set extensions depending on the application.

Because RISC-V is open-source, it can be used for:

- Processor design
- Embedded systems
- System-on-Chip (SoC) development
- Academic and research projects

## SoC Design and OpenLANE

A **System-on-Chip (SoC)** integrates multiple components such as:

- Processor
- Memory
- Peripherals
- Communication interfaces
- IP blocks

All these components are integrated onto a **single semiconductor chip**.

SoC design involves both **RTL design and physical implementation**.

**OpenLANE** is an open-source automated ASIC design flow that converts an RTL design into a physical chip layout.

It integrates multiple open-source EDA tools to automate the **RTL-to-GDSII** process.

## Open-Source EDA Tools

**Electronic Design Automation (EDA)** tools are software tools used to design, verify, and implement electronic circuits and integrated circuits.

Open-source EDA tools provide freely accessible tools for:

- Learning
- Research
- Digital design
- ASIC development

EDA tools are used for different stages of the ASIC design flow, including:

- RTL simulation
- Logic synthesis
- Floorplanning
- Placement
- Clock-Tree Synthesis (CTS)
- Routing
- Parasitic extraction
- Static Timing Analysis (STA)
- Physical verification
- GDSII generation

## RTL-to-GDSII Flow

The **RTL-to-GDSII flow** converts a hardware design written in **Register Transfer Level (RTL)** into a physical layout that can be used for semiconductor fabrication.

The major stages are:

**RTL Preparation → Synthesis → Floorplanning → Placement → Clock-Tree Synthesis → Routing → Physical Verification → GDSII Generation**

Each stage transforms and optimizes the design while checking important:

- Area constraints
- Timing constraints
- Power requirements
- Design rules
- Physical connectivity

The final **GDSII file** represents the physical layout of the chip.

<img src="images/Screenshot-2026-09-13-003852.png" alt="Sky130 Module 5" width="900">

<img src="images/Screenshot%202026-09-13%20003852.png" alt="Sky130 Module 5" width="900">

## Sky130 PDK

The **Sky130 PDK (Process Design Kit)** provides the technology-specific files and libraries required to design circuits using the **SkyWater 130 nm manufacturing process**.

The Sky130 PDK contains:

- Standard-cell libraries
- Technology files
- Design rules
- Timing libraries
- Process information
- Other technology-specific data

The PDK allows EDA tools to understand the characteristics and manufacturing rules of the target semiconductor technology.

Using the **Sky130 PDK**, designers can perform an open-source ASIC design flow based on a real **130 nm semiconductor manufacturing technology**.
# Sky130 Module 2 – Good Floorplan vs Bad Floorplan and Introduction to Library Cells

This module focuses on **ASIC floorplanning, power planning, placement, standard-cell libraries, cell characterization, and timing parameters**. It explains how the physical arrangement of a chip affects **area, performance, power, and routing**.

## Chip Floorplanning

**Floorplanning** is the process of deciding the physical organization of a chip before detailed placement and routing.

It defines:

- Core area
- Die area
- Aspect ratio
- Utilization
- I/O pin locations
- Pre-placed cells
- Power distribution network

A good floorplan provides sufficient space for placement and routing while reducing congestion and improving **timing and power characteristics**.

## Utilization Factor and Aspect Ratio

The **utilization factor** represents the percentage of the core area occupied by standard cells.

**Utilization = Area occupied by cells / Total core area × 100**

Very high utilization can cause:

- Routing congestion
- Timing problems
- Difficult placement
- Limited routing resources

Very low utilization can result in **wasted silicon area**.

The **aspect ratio** is the ratio of the height to the width of the chip or core.

**Aspect Ratio = Height / Width**

Choosing a suitable aspect ratio helps achieve efficient **placement and routing**.

## Pre-Placed Cells

**Pre-placed cells** are important blocks whose physical locations are fixed before standard-cell placement.

Examples include:

- Macros
- Memory blocks
- Large IP blocks
- Other fixed-function blocks

Their locations must be planned carefully because they influence:

- Routing
- Available placement area
- Congestion
- Timing

## Power Planning and Decoupling Capacitors

**Power planning** creates a reliable network for distributing **VDD and VSS/GND** throughout the chip.

The power network must provide sufficient current to all standard cells while minimizing:

- Voltage drop
- IR drop
- Power-related noise
- Reliability problems

**Decoupling capacitors (Decaps)** are placed near cells to provide temporary current during sudden switching activity.

They help reduce:

- Power-supply voltage fluctuations
- Supply noise
- Local voltage instability

## Pin Placement and Placement Blockages

**Pin placement** determines where input and output pins are positioned around the chip boundary.

Proper pin placement helps:

- Reduce wire length
- Reduce routing congestion
- Improve signal connectivity
- Simplify routing

**Placement blockages** are regions where standard cells cannot be placed.

They are useful for protecting reserved areas around:

- Macros
- Power structures
- Critical routing regions
- Fixed cells

## Placement and Library Binding

During placement, standard cells from the technology library are assigned to the logical cells in the synthesized netlist.

The objective is to position cells while optimizing:

- Wire length
- Timing
- Capacitance
- Cell density
- Routing congestion

The placement process starts with an initial placement and progressively optimizes the positions of cells while considering estimated interconnect effects.

## Standard-Cell Libraries and Characterization

A **standard-cell library** contains pre-designed and pre-characterized cells that can be used to implement digital logic.

Common standard cells include:

- AND gates
- OR gates
- NAND gates
- NOR gates
- Inverters
- Flip-flops
- Buffers
- Multiplexers

**Cell characterization** determines the electrical properties of these cells under different operating conditions.

Important characteristics include:

- Timing
- Power consumption
- Input capacitance
- Output behavior
- Propagation delay

The characterized information is stored in library files and is used by EDA tools during:

- Synthesis
- Placement
- Timing analysis
- Optimization

## Congestion-Aware Placement

**Congestion-aware placement** attempts to distribute cells so that sufficient routing resources are available for all connections.

OpenLANE uses **RePlAce** for placement optimization.

The placement process considers factors such as:

- Wire length
- Timing
- Cell density
- Routing congestion
- Interconnect effects

The objective is to obtain a physically efficient placement with better **timing and routability**.

## Cell Design and Characterization Flow

The standard-cell design flow includes:

**Circuit Design → Layout Design → Extraction → Simulation → Characterization**

The circuit is first designed at the **transistor level**.

Then:

1. The physical layout of the cell is created.
2. The layout is verified using design rules.
3. Parasitic information is extracted.
4. The extracted circuit is simulated.
5. The cell is characterized under different conditions.
6. Timing and power information is generated.
7. The characterized data is added to the standard-cell library.

This information is required by EDA tools during the ASIC design flow.

## Timing Characterization

**Timing characterization** determines how quickly a standard cell responds to an input transition and produces the corresponding output transition.

Important timing parameters include:

- Input slew
- Output slew
- Propagation delay
- Setup time
- Hold time
- Timing thresholds

These parameters are essential for predicting circuit performance during **Static Timing Analysis (STA)**.

## Propagation Delay and Transition Time

**Propagation delay** is the time taken for a change at the input of a cell to produce the corresponding change at its output.

Propagation delay depends on factors such as:

- Input slew
- Output load capacitance
- Cell characteristics
- Operating conditions

**Transition time (Slew)** represents how quickly a signal changes between defined voltage levels.

Both propagation delay and transition time are important for determining the **timing performance and signal quality** of a digital circuit.
# OpenLANE Module 2 – Commands

## 1. Start OpenLANE

Start OpenLANE in interactive mode from the OpenLANE flow directory.

```bash
cd /openLANE_flow
./flow.tcl -interactive
```
## 2. Load the Design

Before running the physical design stages, the required design must be loaded and prepared.

## Command

```tcl
package require openlane
prep -design <design_name>
```
## 3. Run Floorplanning

After preparing the design, the floorplanning stage can be executed.

## Command

```tcl
run_floorplan
```
## 4. Run Placement

After floorplanning, standard cells are placed inside the core area.

## Command

```tcl
run_placement
```
## 5. Run Placement with Verbose Output

Placement can also be executed with detailed information.

## Command

```tcl
run_placement -verbose
```
## 6. Run the Complete OpenLANE Flow

Instead of executing each stage manually, the **complete OpenLANE RTL-to-GDSII flow** can be run automatically.

## Command

```bash
./flow.tcl -design <design_name>
```
## 7. View the Floorplan in Magic

The generated floorplan can be viewed and inspected using **Magic**, an open-source VLSI layout tool.

## Command

```bash
magic -T <tech_file> <def_file>
```
# Sky130 Module 3 – Design Library Cell Using Magic Layout and ngspice Characterization

## Introduction

Sky130 Module 3 focuses on the complete design, simulation, layout, verification, and characterization of a CMOS standard cell using open-source VLSI tools.

The main tools used in this module are `Magic` and `ngspice`. `Magic` is used for physical layout and design-rule checking, while `ngspice` is used for circuit simulation and electrical characterization.

The module mainly explains how a CMOS inverter is converted from a circuit-level design into a physical standard-cell layout and how the layout is verified and simulated.

## CMOS Inverter

A CMOS inverter is one of the most basic and important digital logic cells. It consists of two MOS transistors:

* `PMOS` transistor at the top connected to `VDD`.
* `NMOS` transistor at the bottom connected to `GND`.

The gates of both transistors are connected to the input, and their drains are connected together to form the output.

When the input is `LOW`, the PMOS turns `ON` and the NMOS turns `OFF`. Therefore, the output becomes `HIGH`.

When the input is `HIGH`, the PMOS turns `OFF` and the NMOS turns `ON`. Therefore, the output becomes `LOW`.

The CMOS inverter is widely used as a basic building block for logic gates, buffers, oscillators, and other digital circuits.

## ngspice Simulation

`ngspice` is an open-source circuit simulator used to analyze the electrical behavior of electronic circuits.

For the CMOS inverter, `ngspice` can simulate the relationship between input and output voltages and determine important characteristics of the circuit.

The simulation helps to study:

* Input and output voltage behavior
* Voltage Transfer Characteristic
* Switching threshold
* Propagation delay
* Rise time
* Fall time
* Power consumption

The simulation results help verify whether the designed inverter behaves correctly before creating its physical layout.

## SPICE Deck

A `SPICE deck` is a text-based description of a circuit that can be understood by a SPICE simulator.

For a CMOS inverter, the SPICE deck contains the transistor definitions, node connections, power supply, input signal, output node, transistor model files, and simulation commands.

The basic structure represents the PMOS and NMOS transistors and their connections between `VDD`, input, output, and ground.

Sky130 transistor model files are included so that `ngspice` can simulate the circuit according to the characteristics of the Sky130 fabrication technology.

## Inverter Characterization

Characterization means measuring the important electrical and timing properties of a standard cell through simulation.

For a CMOS inverter, characterization determines how the cell responds to different input signals.

Important parameters include:

* Switching threshold voltage
* Propagation delay
* Rise time
* Fall time
* Input capacitance
* Output behavior
* Power consumption

These values are important because standard-cell libraries require timing and electrical information for tools such as synthesis, placement, routing, and static timing analysis.

## Switching Threshold

The switching threshold, commonly represented as `Vm`, is the input voltage at which the CMOS inverter changes its logic state.

At the switching point, the PMOS and NMOS devices conduct simultaneously and the inverter output is approximately equal to the input voltage.

The switching threshold is important for understanding the noise tolerance and logic behavior of the inverter.

A properly designed CMOS inverter should provide clear separation between logic `LOW` and logic `HIGH`.

## Static and Dynamic Behavior

Static analysis studies the DC behavior of the CMOS inverter.

The `Voltage Transfer Characteristic (VTC)` is used to observe how the output voltage changes with the input voltage. It helps determine the logic `LOW`, logic `HIGH`, switching threshold, and noise margins.

Dynamic analysis studies the behavior of the inverter when the input changes with time.

Important dynamic parameters include:

* Rise time
* Fall time
* Propagation delay

These parameters are especially important in digital circuits because they determine how quickly a signal can travel through a logic cell.

## CMOS Layout Using Magic

`Magic` is an open-source VLSI layout tool used to create and inspect the physical layout of integrated circuits.

In the CMOS inverter layout, different Sky130 technology layers are used to represent the physical structures of the transistors and their connections.

The layout generally contains:

* `N-well` region for the PMOS
* P-type or substrate region for the NMOS
* Diffusion regions for source and drain
* `Polysilicon` for transistor gates
* Contacts for connecting different layers
* Metal layers for electrical connections
* Power and ground connections

The physical layout must follow the design rules specified by the Sky130 technology.

## CMOS Fabrication Concept

The layout layers correspond to physical manufacturing steps used to create CMOS transistors on a silicon wafer.

The basic process includes creating active regions, forming wells, defining the polysilicon gate, creating source and drain regions, forming contacts, and adding metal interconnections.

The `N-well` provides the region in which the PMOS transistor is formed, while the NMOS transistor is formed in the appropriate P-type region.

The polysilicon crossing the active region forms the transistor gate.

Source and drain regions are formed on either side of the gate.

Contacts and metal layers are then used to connect the devices to `VDD`, `GND`, input, and output.

Understanding this process helps in understanding how the physical layout represents the actual CMOS circuit.

## Design Rule Checking

`Design Rule Checking (DRC)` is used to verify whether the physical layout follows the manufacturing rules of the Sky130 process.

`Magic` can perform DRC and identify geometrical errors in the layout.

Typical DRC checks include:

* Minimum layer width
* Minimum spacing between layers
* Required overlap between layers
* Contact size and enclosure
* Spacing between polysilicon and diffusion
* Spacing between metal layers

Correcting these errors is necessary before the layout can be considered fabrication-ready.

## SPICE Netlist Extraction

After the layout is completed and verified, the physical layout can be converted into a SPICE representation.

`Magic` can extract the circuit information from the layout and generate an extracted SPICE netlist.

The extracted netlist contains information about:

* Transistors
* Parasitic elements
* Nodes
* Electrical connections

This netlist can be simulated using `ngspice` to verify that the physical implementation behaves correctly.

## Layout Versus Circuit Behavior

The original CMOS inverter is first simulated at the circuit level.

After creating the physical layout, the layout is extracted into a SPICE netlist and simulated again.

Comparing the two simulations helps identify the effect of the physical implementation.

The extracted circuit may show differences in timing and electrical behavior because the physical layout introduces parasitic capacitance and resistance.

Therefore, `post-layout simulation` provides a more realistic representation of the actual cell behavior.

## Standard Cell

A `standard cell` is a pre-designed and characterized logic block that can be reused during digital IC design.

Examples include:

* Inverter
* Buffer
* NAND gate
* NOR gate
* AND gate
* OR gate
* Flip-flop

A standard cell normally contains:

* Physical layout
* Logical information
* Timing information
* Technology-specific data

The CMOS inverter studied in this module serves as a basic example of how such a standard cell is designed and characterized.

## Overall Module Flow

```text
CMOS Circuit Design
        ↓
SPICE Deck Creation
        ↓
ngspice Simulation
        ↓
CMOS Inverter Characterization
        ↓
Magic Physical Layout
        ↓
Sky130 Design Rules
        ↓
DRC Verification
        ↓
SPICE Netlist Extraction
        ↓
Post-Layout ngspice Simulation
        ↓
Standard Cell Characterization
        ↓
Library Cell
```
# Sky130 Module 4 – Pre-layout Timing Analysis and Importance of Good Clock Trees

## Introduction

Sky130 Module 4 focuses on timing analysis, timing libraries, setup and hold timing, clock tree synthesis, and timing analysis using ideal and real clocks.

The main tools used in this module include `OpenSTA`, `OpenROAD`, `TritonCTS`, `Magic`, and Sky130 timing libraries.

The module explains how the timing behavior of standard cells is represented using delay tables and timing libraries, how setup and hold violations are identified, and how clock trees are designed and optimized for reliable timing.

## Timing Analysis

Timing analysis is used to determine whether signals in a digital circuit reach their destination within the required time.

A digital circuit contains combinational logic and sequential elements such as flip-flops. Data must travel from one flip-flop to another within a specific timing window.

The main timing parameters are:

* Propagation delay
* Setup time
* Hold time
* Clock skew
* Clock uncertainty
* Clock latency
* Slack

Timing analysis helps determine whether a design can operate correctly at the required clock frequency.

## Delay Tables

Delay tables are used to represent the delay characteristics of standard cells.

The delay of a cell depends mainly on input transition time and output load capacitance.

A timing library contains tables that provide delay values for different combinations of input slew and output load.

This allows synthesis and timing-analysis tools to estimate the delay of cells without performing transistor-level simulation for every circuit operation.

For example, a cell may have different propagation delays for:

* Small input slew and small load
* Small input slew and large load
* Large input slew and small load
* Large input slew and large load

The tool uses these values to estimate the timing of the complete design.

## Timing Libraries

A timing library contains electrical and timing information about standard cells.

The library can contain information such as:

* Cell functionality
* Input capacitance
* Output capacitance
* Propagation delay
* Rise and fall delay
* Rise and fall transition
* Setup time
* Hold time
* Power information

This information is required by synthesis and static timing analysis tools to make timing-aware design decisions.

Sky130 provides technology-specific timing libraries for different process, voltage, and temperature conditions.

## Standard Cell LEF

`LEF` stands for `Library Exchange Format`.

It provides physical information about a standard cell that is required by physical-design tools.

A LEF file generally contains:

* Cell dimensions
* Pin locations
* Pin names
* Pin directions
* Routing layers
* Routing information
* Obstructions

The LEF does not contain the complete detailed transistor-level layout. Instead, it provides an abstract physical representation that tools can use during placement and routing.

Converting a Magic layout into a standard-cell LEF allows the cell to be used by digital implementation tools.

## Pre-layout Timing Analysis

Pre-layout timing analysis is performed before the final physical layout and detailed routing are completed.

At this stage, the design is analyzed using estimated delays and idealized physical information.

The purpose is to identify timing problems early in the design process.

If timing violations are found, synthesis settings, cell selection, buffering, or logic structure can be modified before proceeding further into physical implementation.

Pre-layout timing analysis therefore helps reduce the effort required to fix timing problems later.

## Slack

Slack is the difference between the required arrival time and the actual arrival time of a signal.

For setup analysis:

`Slack = Required Arrival Time − Actual Arrival Time`

* Positive slack means the signal meets the timing requirement.
* Zero slack means the signal reaches the required timing limit.
* Negative slack indicates a timing violation.

The objective of timing optimization is generally to eliminate negative slack and achieve positive timing margins.

## Setup Time

Setup time is the minimum amount of time that data must remain stable before the active clock edge of a flip-flop.

If data arrives too late, the flip-flop may not capture the correct value.

A setup violation occurs when the data arrival time is later than the allowed setup requirement.

Setup timing can be improved by:

* Reducing data-path delay
* Using faster cells
* Optimizing logic
* Modifying the clock period

## Hold Time

Hold time is the minimum amount of time that data must remain stable after the active clock edge.

If data changes too quickly after the clock edge, the flip-flop may capture incorrect data.

A hold violation occurs when data reaches the destination flip-flop too early.

Hold violations can be corrected by:

* Adding delay to the data path
* Using appropriate cells
* Optimizing the clock path

## Clock Jitter and Uncertainty

Clock jitter refers to the variation of the clock edge from its ideal position in time.

Clock uncertainty represents the timing margin reserved for effects such as clock jitter, skew, and other variations.

Including clock uncertainty in timing analysis makes the analysis more realistic.

A larger uncertainty reduces the available timing margin and can make timing closure more difficult.

## OpenSTA Timing Analysis

`OpenSTA` is an open-source Static Timing Analysis tool.

It analyzes the timing behavior of a digital circuit without applying every possible input combination through simulation.

OpenSTA uses:

* Netlist
* Timing libraries
* SDC constraints
* Clock definitions
* Input and output constraints

The tool calculates:

* Arrival times
* Required times
* Slack
* Setup violations
* Hold violations

This makes it useful for identifying critical timing paths in a synthesized design.

## Timing Optimization

If timing violations are present, synthesis can be optimized to improve the design.

Common methods include:

* Using faster standard cells
* Increasing cell drive strength
* Adding buffers
* Reducing logic depth
* Optimizing critical paths
* Changing synthesis constraints
* Reducing excessive load capacitance

The objective is to improve timing while maintaining acceptable area and power.

## Timing ECO

`ECO` stands for `Engineering Change Order`.

A timing ECO is a small modification made to the existing design to correct timing problems without completely redesigning the circuit.

Typical timing ECO operations include:

* Cell resizing
* Cell replacement
* Buffer insertion
* Buffer removal
* Changing the drive strength of a cell
* Adding delay cells for hold fixing

Timing ECOs are useful during the final stages of design when only a few timing violations remain.

## Clock Tree Synthesis

`Clock Tree Synthesis (CTS)` is the process of creating a clock distribution network from the clock source to all required sequential elements.

A clock signal must reach different flip-flops with controlled delay and minimal skew.

CTS inserts buffers and creates a structured network to distribute the clock.

A good clock tree should provide:

* Low clock skew
* Controlled clock latency
* Good signal integrity
* Balanced clock paths
* Reliable clock transitions

## H-Tree Clock Distribution

An `H-tree` is a commonly used clock distribution structure.

The clock source is placed at the center and the clock network branches symmetrically.

The branches form an H-shaped structure and continue recursively until the clock reaches the required destinations.

Because of its symmetrical structure, an H-tree can help reduce differences in clock path length and therefore reduce clock skew.

## Clock Skew

Clock skew is the difference in clock arrival time between two sequential elements.

If the clock reaches one flip-flop earlier than another, the difference is called clock skew.

Large clock skew can cause setup or hold timing problems.

CTS attempts to balance clock paths and minimize undesirable skew.

Good clock-tree design is therefore essential for reliable sequential-circuit operation.

## Clock Buffering

Clock buffers are inserted into the clock network to drive the large capacitive load created by multiple flip-flop clock pins and long clock wires.

Without proper buffering, the clock signal can experience:

* Large delay
* Slow transition
* Signal degradation
* High power consumption
* Poor timing

Clock buffers help maintain a strong and properly timed clock signal throughout the design.

## Crosstalk and Clock Shielding

Crosstalk occurs when a signal on one wire affects a nearby signal because of capacitive or inductive coupling.

Clock networks are especially sensitive because the clock is a high-fanout and timing-critical signal.

Clock shielding can be used to reduce unwanted coupling from nearby signal wires.

Shielding typically places a stable power or ground wire near the clock route to reduce interference.

This improves clock signal integrity and helps maintain reliable timing.

## TritonCTS

`TritonCTS` is a clock tree synthesis tool used in the OpenROAD flow.

It automatically constructs the clock distribution network by inserting clock buffers and connecting clock sinks.

The goal is to achieve acceptable clock latency and skew while considering the physical characteristics of the design.

CTS is normally performed after placement and before detailed routing.

## Ideal Clock Analysis

In ideal-clock timing analysis, the clock is assumed to reach the sequential elements without considering the actual physical clock-tree delay and skew.

This provides an early understanding of the design's timing behavior.

Ideal-clock analysis is useful during the pre-CTS stage because it allows timing problems in the logic/data paths to be identified before the actual clock tree is constructed.

## Real Clock Analysis

After CTS, the clock is distributed through actual buffers and physical wires.

Timing analysis using these propagated clock paths is called real-clock or propagated-clock analysis.

Real-clock analysis considers effects such as:

* Clock insertion delay
* Clock skew
* Clock buffer delays
* Clock wire delays
* Clock transitions

This provides a more realistic picture of the final timing behavior of the design.

## Setup Timing with Real Clocks

After CTS, setup timing is analyzed using the actual propagated clock.

The data path must reach the destination flip-flop early enough to satisfy the setup requirement.

Clock skew can either improve or worsen setup timing depending on the relative arrival times of the launch and capture clocks.

Therefore, setup timing must be checked again after CTS.

## Hold Timing with Real Clocks

Hold timing is also analyzed after CTS using the actual clock network.

The data must not arrive too early at the destination flip-flop after the active clock edge.

Clock skew can have a significant effect on hold timing.

A design that passes hold analysis with ideal clocks may develop hold violations after CTS because the actual clock arrival times are different.

Therefore, both setup and hold timing must be verified using propagated clocks.

## Importance of a Good Clock Tree

A good clock tree is essential for reliable digital circuit operation.

An improperly designed clock tree can cause:

* Setup violations
* Hold violations
* Large clock skew
* Excessive clock latency
* Poor signal integrity
* Increased clock power

A well-balanced clock tree helps ensure that clock signals reach sequential elements with controlled delay and minimum unwanted skew.

## Overall Module Flow

```text
Standard Cell Timing Information
        ↓
Delay Tables and Timing Libraries
        ↓
Standard Cell LEF
        ↓
Synthesis
        ↓
Pre-layout Timing Analysis
        ↓
Setup and Hold Analysis
        ↓
Timing Optimization
        ↓
Placement
        ↓
Clock Tree Synthesis using TritonCTS
        ↓
Clock Buffering and Clock Routing
        ↓
Real Clock Timing Analysis
        ↓
Setup and Hold Verification
        ↓
Timing Closure
```
# Sky130 Module 5 – Final Steps for RTL to GDS Using Triton Route and OpenSTA

## Introduction

Sky130 Module 5 focuses on the final stages of the RTL-to-GDSII flow. The main topics are power distribution, global and detailed routing, TritonRoute, routing algorithms, design rule checking, and final timing analysis using OpenSTA.

Routing connects all the placed standard cells, macros, power networks, and I/O pins according to the logical connectivity of the design.

The main tools involved in this stage are `TritonRoute` for detailed routing and `OpenSTA` for final static timing analysis.

## Routing

Routing is the process of creating physical connections between the cells and pins after placement.

The routing stage converts the logical connections from the netlist into actual metal-layer wires and vias.

The main objectives of routing are:

* Connecting all required nets.
* Following technology design rules.
* Minimizing wire length.
* Reducing congestion.
* Maintaining signal integrity.
* Meeting timing requirements.

The routing process is generally divided into global routing and detailed routing.

## Global Routing

Global routing determines the general path that each net should follow through the available routing regions.

Instead of immediately creating exact wire geometries, global routing divides the chip into routing regions and determines suitable paths between them.

Global routing considers:

* Routing congestion.
* Available routing resources.
* Approximate wire length.
* Connectivity.
* Different routing layers.

The result provides routing guidance that is later used by the detailed router.

## Detailed Routing

Detailed routing converts the global routing information into actual physical wires and vias.

It determines the exact:

* Wire locations.
* Wire widths.
* Via locations.
* Routing layers.
* Connections between pins.

Detailed routing must follow the design rules of the Sky130 technology.

`TritonRoute` is used for detailed routing in the OpenLANE/OpenROAD flow.

## Maze Routing

Maze routing is a routing technique used to find a path between two points while avoiding obstacles.

One of the well-known maze-routing methods is Lee's algorithm.

The algorithm explores the routing area step by step until it finds a path from the source to the destination.

The basic process is:

* Start from the source.
* Expand to neighboring locations.
* Assign distance values.
* Continue expansion until the destination is reached.
* Trace the path back to the source.

Maze routing can find a valid path even when obstacles make the routing problem complicated.

## Lee's Algorithm

Lee's algorithm is a grid-based routing algorithm.

The routing area is represented as a grid. Each grid location is assigned a distance value as the search progresses.

The algorithm first marks the source location and expands to neighboring locations.

When the destination is reached, the algorithm traces backward through the distance values to obtain the shortest available path.

The main advantage of Lee's algorithm is that it can find a guaranteed path when one exists.

However, it can require significant memory and computation for large routing areas.

## Power Distribution Network

The Power Distribution Network, or PDN, distributes power and ground throughout the chip.

The main power networks are:

* `VDD` for the positive supply.
* `VSS` or `GND` for the ground connection.

A properly designed PDN ensures that standard cells and other circuit blocks receive a stable power supply.

The PDN generally consists of power rings, power straps, rails, and connections to standard-cell power pins.

## Power Straps

Power straps are wide metal structures used to distribute `VDD` and `VSS` across the chip.

They connect the higher-level power network to the lower-level power rails used by standard cells.

Power straps help reduce:

* IR drop.
* Voltage fluctuations.
* Power distribution problems.

They also provide a low-resistance path for delivering current to different regions of the chip.

## Standard Cell Power Connections

Standard cells require connections to `VDD` and `VSS`.

The power distribution network connects the higher-level power straps to the standard-cell power rails.

This creates a continuous power path from the chip-level power network to individual standard cells.

Proper power connectivity is necessary for reliable operation of the entire design.

## TritonRoute

`TritonRoute` is an open-source detailed routing engine used in the OpenROAD flow.

It takes the placement and routing information and creates physical routes between connected pins.

TritonRoute considers:

* Routing guides.
* Design-rule constraints.
* Routing layers.
* Wire connections.
* Via placement.
* Signal connectivity.

Its objective is to create legal and complete routes while satisfying the technology constraints.

## TritonRoute Routing Guides

Routing guides provide information about the preferred regions through which a net should be routed.

TritonRoute can use pre-processed route guides generated during the global-routing stage.

These guides help the detailed router understand the intended routing regions and reduce unnecessary exploration.

This improves routing efficiency and helps maintain the routing plan produced by the earlier routing stage.

## Inter-Guide Connectivity

A single net may have multiple routing guides.

Inter-guide connectivity refers to connecting different routing-guide regions belonging to the same net.

The router must create valid connections between these regions so that the entire net becomes electrically connected.

This is important for nets that span multiple routing regions.

## Intra-Layer and Inter-Layer Routing

Routing can occur within the same metal layer or between different metal layers.

Intra-layer routing connects shapes on the same routing layer.

Inter-layer routing moves a connection from one metal layer to another using vias.

Using multiple metal layers provides additional routing resources and helps reduce congestion.

## Connectivity Handling

The routing system must ensure that every required connection in the design is physically completed.

TritonRoute checks whether the routed wires correctly connect:

* Cell pins.
* Input and output pins.
* Power connections.
* Other connected components.

The final routed design should not contain disconnected nets or unintended connections.

## Routing Topology

Routing topology describes the structure or arrangement used to connect multiple pins belonging to the same net.

For a net with multiple pins, the router must determine an efficient topology that connects all pins.

A good routing topology helps reduce:

* Wire length.
* Routing congestion.
* Number of vias.
* Delay.
* Power consumption.

The topology is then converted into physical wires and vias during detailed routing.

## Design Rule Check

Design Rule Checking, or DRC, verifies whether the final physical layout satisfies the manufacturing rules of the Sky130 process.

DRC checks geometrical properties such as:

* Minimum wire width.
* Minimum spacing.
* Via rules.
* Metal spacing.
* Layer overlap.
* Enclosure requirements.

A design with DRC violations may not be suitable for fabrication.

Therefore, DRC is an important final verification step after routing.

## Final Timing Analysis Using OpenSTA

After routing is completed, the actual physical interconnect information can be used for final timing analysis.

`OpenSTA` performs Static Timing Analysis on the routed design.

It checks important timing parameters such as:

* Setup slack.
* Hold slack.
* Clock skew.
* Data arrival time.
* Required arrival time.
* Critical paths.

The final timing analysis helps determine whether the routed design can operate at the required clock frequency.

## RTL-to-GDSII Final Flow

The complete physical-design flow reaches its final stages as follows:

```text
RTL Design
    ↓
Synthesis
    ↓
Floorplanning
    ↓
Placement
    ↓
Clock Tree Synthesis
    ↓
Global Routing
    ↓
Detailed Routing using TritonRoute
    ↓
DRC Verification
    ↓
Parasitic Extraction
    ↓
Final Timing Analysis using OpenSTA
    ↓
GDSII
