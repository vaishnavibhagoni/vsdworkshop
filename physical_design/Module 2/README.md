# Module 2 — Good Floorplan vs Bad Floorplan and Introduction to Library Cells

## Overview

Module 2 moves from the introductory RTL-to-GDSII flow into physical organization of the chip. The module covers floorplanning, utilization, aspect ratio, pre-placed cells, decoupling capacitors, power planning, pin placement and placement blockages. It then moves into library binding, placement optimization, standard-cell design and characterization, and basic timing-characterization parameters.

OpenLANE is used to run and inspect the floorplan, while Magic is introduced for visual inspection of the physical layout.

## Learning Objectives

- Understand why floorplanning is performed before detailed placement and routing.
- Explain utilization factor and aspect ratio and their relationship to available placement area.
- Understand the purpose of pre-placed cells and decoupling capacitors.
- Understand basic power-planning and pin-placement considerations.
- Explain how a synthesized netlist is bound to physical library cells.
- Understand placement optimization using estimated wire-length and capacitance.
- Explain the role of congestion-aware placement and RePlAce.
- Describe the basic standard-cell design and characterization flow.
- Understand timing thresholds, propagation delay and transition time.

## Topics Covered

### SKY130_D2_SK1 — Chip Floor Planning Considerations

- Utilization factor and aspect ratio
- Concept of pre-placed cells
- De-coupling capacitors
- Power planning
- Pin placement and logical cell placement blockage
- Steps to run floorplan using OpenLANE
- Review floorplan files and steps to view floorplan
- Review floorplan layout in Magic

### SKY130_D2_SK2 — Library Binding and Placement

- Netlist binding and initial place design
- Optimize placement using estimated wire-length and capacitance
- Final placement optimization
- Need for libraries and characterization
- Congestion-aware placement using RePlAce

### SKY130_D2_SK3 — Cell Design and Characterization Flows

- Inputs for cell design flow
- Circuit design step
- Layout design step
- Typical characterization flow

### SKY130_D2_SK4 — General Timing Characterization Parameters

- Timing threshold definitions
- Propagation delay and transition time

## Floorplanning Concepts

### Utilization Factor

Utilization describes how much of the available core area is occupied by placed standard-cell area. Very high utilization can reduce available routing space and increase congestion, while very low utilization can waste silicon area.

### Aspect Ratio

Aspect ratio describes the relationship between the height and width of the core or die. The chosen aspect ratio affects physical organization, routing resources and overall chip shape.

### Pre-placed Cells

Some cells or macros must be placed at predetermined locations or regions before standard-cell placement. Their positions influence available placement and routing resources.

### Decoupling Capacitors

Decoupling capacitors are included as part of power integrity considerations. They help provide local charge during switching activity and reduce undesirable power-supply variations.

### Pin Placement and Blockages

I/O pin locations and placement blockages affect how signals enter and leave the core and where standard cells can be legally placed. These decisions therefore influence routability and congestion.

## Placement Flow

```text
Synthesized Netlist
        ↓
Library Binding
        ↓
Initial Placement
        ↓
Wire-Length / Capacitance Estimation
        ↓
Placement Optimization
        ↓
Congestion-Aware Placement
        ↓
Final Placement
```

## Standard-Cell Characterization

A standard cell needs characterized timing information so that implementation and timing-analysis tools can estimate its behavior under different conditions. The module introduces the flow from circuit design to layout and characterization, followed by parameters such as timing thresholds, propagation delay and transition time.

## Figures and Practical Evidence

### 1. Floorplan and Physical Organization

<img width="1275" height="775" alt="image" src="https://github.com/user-attachments/assets/6d212a96-36d5-40df-ae4e-b54420995694" />

<img width="1278" height="781" alt="image" src="https://github.com/user-attachments/assets/952b86df-c000-48aa-aaa9-415e4d978865" />

<img width="1618" height="1050" alt="image" src="https://github.com/user-attachments/assets/2fd3197f-8bd0-4482-a5fd-07767b6ab9de" />

<img width="1915" height="1095" alt="image" src="https://github.com/user-attachments/assets/a785ad7c-7895-4816-b838-63c90ff4949d" />

<img width="1885" height="1080" alt="image" src="https://github.com/user-attachments/assets/2c3a43c0-d92c-4d71-8484-c092257c8a12" />

<img width="1288" height="770" alt="image" src="https://github.com/user-attachments/assets/9d45125c-0f06-4246-9614-b970548904c5" />




### 2. Placement and Library Binding

<img width="1753" height="1102" alt="image" src="https://github.com/user-attachments/assets/07bd1b6b-f03a-4475-9da1-66de586e0342" />

<img width="1907" height="1107" alt="image" src="https://github.com/user-attachments/assets/12427754-811e-4b9f-8813-8975937f9bc5" />
<img width="1912" height="1007" alt="image" src="https://github.com/user-attachments/assets/7c2965d9-e4d3-44ec-badd-22651628a220" />


### 3. Cell Design and Characterization

<img width="1900" height="1097" alt="image" src="https://github.com/user-attachments/assets/5c097c68-a52c-4055-bd4c-48f82bcd6116" />

<img width="1902" height="1042" alt="image" src="https://github.com/user-attachments/assets/20f08010-262c-40b0-902c-4eaa53f1a6d1" />

<img width="1917" height="1117" alt="image" src="https://github.com/user-attachments/assets/1265649f-88f3-4282-8a20-186de1b3b9d5" />



### 4. Metal-Layer Examples

<img width="1281" height="767" alt="image" src="https://github.com/user-attachments/assets/350e6327-236b-4a03-bfca-a28faf7ce908" />

<img width="1282" height="766" alt="image" src="https://github.com/user-attachments/assets/6243e7a3-4ea1-4305-bd93-d42872c4dad0" />


## Practical Workflow in OpenLANE

The practical sequence introduced in this module is to prepare the design, configure the floorplan-related settings, run the floorplan stage, inspect generated files and then visualize the resulting layout in Magic. Placement is subsequently considered in terms of library binding, optimization and congestion.

## Key Takeaways

- Floorplanning determines the initial physical organization of the design.
- Utilization and aspect ratio directly affect available physical resources.
- Macros, pre-placed cells, power structures, pins and blockages must be considered before detailed placement.
- Placement is not simply putting cells into empty locations; wire-length, capacitance and congestion must also be considered.
- Standard-cell characterization supplies timing information needed by implementation tools.
- Propagation delay and transition time are important parameters when describing cell timing behavior.

## Tools / Technologies

- OpenLANE
- Magic
- Sky130 standard-cell libraries
- RePlAce placement engine
- Linux / Ubuntu
