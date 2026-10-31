
# Physical Design

This section presents the practical implementation of the **VSDBabySoC** design through the different stages of digital ASIC physical design, beginning with synthesis and continuing through routing and timing verification.

The documentation is prepared based on the screenshots and observations collected during the lab sessions. It is maintained as a separate portfolio folder, where this README introduces the overall work, `reports/` contains detailed descriptions of individual stages, and `images/` stores the screenshots captured during the implementation process.

## Lab at a glance

| Item | Details |
|---|---|
| Design | VSDBabySoC |
| Technology | Sky130HD |
| Physical Design Environment | OpenROAD Flow |
| Timing Analysis Tool | OpenSTA |
| Evidence Included | Synthesis results, floorplanning, placement, CTS, routing, setup and hold timing screenshots, and configuration details |

## What this lab covers

The main objective of this lab is to understand the complete physical implementation process and how an RTL design is converted into a physically structured ASIC layout. Each stage performs a specific operation and contributes to the overall design implementation.

1. **Synthesis** — transform the RTL code into a gate-level netlist using the selected technology library.
2. **Floorplanning** — determine the core and die dimensions and plan the arrangement of I/O pins and other physical resources.
3. **Placement** — position standard cells within the core area while considering the physical organization of the design.
4. **Clock Tree Synthesis (CTS)** — create the clock distribution network by inserting suitable buffers to distribute the clock signal.
5. **Routing** — establish electrical connections between the placed cells using metal layers and vias.
6. **Post-route Timing Analysis** — analyze setup and hold paths using OpenSTA to evaluate the timing performance of the final implementation.

## Workflow and observations

### 1. Synthesis and design setup

Synthesis is the starting point for physical implementation: RTL is mapped into library cells, producing a netlist and implementation database for downstream steps. The package includes a synthesis output screenshot and configuration screenshots that show the design setup used in the OpenROAD flow.



<img width="1920" height="848" alt="01_synthesis_output" src="https://github.com/user-attachments/assets/e77227da-0d04-4d5a-a36a-283a2f4d7012" />



### 2. Floorplan

The floorplan establishes the die/core organization, margins, and a starting arrangement for physical implementation. The included GUI screenshots show the floorplan and a saved database view.

<img width="1920" height="865" alt="02_floorplan_gui" src="https://github.com/user-attachments/assets/fc550b56-7e51-42a1-a4c6-180d283a4e51" />

<img width="1592" height="843" alt="02_floorplan_database" src="https://github.com/user-attachments/assets/b03151bd-3a02-4983-90f3-9c4f12580e4e" />

### 3. Placement

Placement assigns locations to standard cells. The supplied views include a full placement view, alternate layer and terminal views, and a zoomed-out view. These are useful for observing the physical arrangement at different scales; they are not, by themselves, a numeric placement-quality report.



<img width="1920" height="900" alt="03_placement_gui" src="https://github.com/user-attachments/assets/5adfee8f-db92-4ef1-b9b1-5eac48181743" />



### 4. Clock-tree synthesis

CTS creates a network to distribute the clock to sequential elements. The lab screenshots contain full-design and close-up views of the resulting layout, as well as a selected clock-buffer instance. The images document inspection of the clock network, but no numerical clock-skew summary was supplied.


<img width="1600" height="814" alt="04_cts_fullview" src="https://github.com/user-attachments/assets/c18046d8-ec3e-4941-8f99-f765d5d19cee" />

<img width="1600" height="546" alt="cts_clock_buffer_detail" src="https://github.com/user-attachments/assets/adcacb41-7273-430b-9ad7-816f2da7ecc7" />

### 5. Routing

Routing connects the placed instances using the available interconnect layers and vias. The supplied images show both a whole-design routing view and a more detailed view of the metal geometry.


<img width="1595" height="870" alt="05_routing_full_view" src="https://github.com/user-attachments/assets/c6ce9105-160c-44a4-a2eb-893d474bd018" />

<img width="1920" height="885" alt="08_routing_detailed_view" src="https://github.com/user-attachments/assets/8c731f39-3d37-43ab-b011-1cd1e6842c25" />


 The supplied package does not include an authoritative route summary file from which to report total wire length, via count, DRC count, or antenna violations; those numeric fields are therefore intentionally not inferred.

### 6. OpenSTA timing review

The supplied OpenSTA screenshots show timing-path reports for a maximum-delay (setup-oriented) path and a minimum-delay (hold-oriented) path.


<img width="1920" height="903" alt="06_opensta_setup_timing" src="https://github.com/user-attachments/assets/e95be340-e277-478d-82f7-15423cc5cfb7" />

<img width="1920" height="883" alt="07_opensta_hold_timing" src="https://github.com/user-attachments/assets/acce7f62-a64f-447f-aa1f-3d8f2cb80ed9" />

The screenshots visibly show positive slack values for the displayed paths:
- Setup-oriented path: **7.35 slack (MET)**.
- Hold-oriented path: **0.28 slack (MET)**.

These are the slack values shown for the individual paths in the provided images, not a complete worst-slack summary for every path in the design. The accompanying reference notes report `WNS max = 0.00` and `TNS max = 0.00`; those values are preserved in the dedicated OpenSTA report as notes from the reference context, rather than being substituted for the path slack shown in the screenshots. To establish a single definitive timing summary, rerun/report the design using the exact final timing database, constraints, and parasitics.


## Tools and concepts encountered

- **OpenROAD** — physical-design implementation and GUI inspection.
- **OpenSTA** — static timing analysis of design paths.
- **Sky130HD** — standard-cell technology library referenced by the lab.
- **Floorplan, placement, CTS and routing** — sequential stages that transform a synthesized netlist into a connected physical layout.
- **Setup and hold timing** — complementary checks for data-path timing relative to the clock.

## Scope and data integrity

This is a report package assembled from the images and the supplied reference notes, not a regenerated OpenROAD run. It does not claim that the tools were re-executed here. Reported metrics are limited to what can be verified in the provided material; unavailable design statistics are marked as not supplied rather than guessed.

## Author / academic context

**B.Vaishnavi**  
**25EG504H17**
B.Tech, III Year — Electronics and Communication Engineering  
Anurag University
