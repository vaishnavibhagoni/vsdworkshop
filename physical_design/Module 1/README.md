# Module 1 — Inception of Open-Source EDA, OpenLANE and Sky130 PDK

## Overview

Module 1 establishes the foundation for the Physical Design workshop. It starts with the relationship between software and hardware, introduces chips, packages, pads, cores, dies and IPs, and then moves into RISC-V, SoC design, open-source EDA, the Sky130 PDK and the OpenLANE RTL-to-GDSII flow.

The practical part introduces the OpenLANE directory structure, design-preparation stage, synthesis, generated netlists and basic interpretation of synthesis results. These concepts form the base for the floorplanning, placement, timing and routing work covered in later modules.

## Learning Objectives

By the end of this module, the learner should be able to:

- Explain the basic structure of a digital IC from package and chip level down to the core and IP blocks.
- Relate software applications, compilers, RTL and hardware implementation.
- Describe the role of RISC-V in an open instruction-set architecture ecosystem.
- Identify the major components of an open-source digital ASIC flow.
- Explain the simplified RTL-to-GDSII flow and the purpose of OpenLANE.
- Understand why a PDK is required for technology-specific physical implementation.
- Navigate the important parts of an OpenLANE project directory.
- Understand the purpose of design preparation and synthesis.
- Inspect a generated synthesis netlist and basic synthesis statistics.

## Topics Covered

### SKY130_D1_SK1 — How to talk to computers

- Introduction to QFN-48 package, chip, pads, core, die and IPs
- Introduction to RISC-V
- From software applications to hardware

### SKY130_D1_SK2 — SoC design and OpenLANE

- Introduction to all components of open-source digital ASIC design
- Simplified RTL2GDS flow
- Introduction to OpenLANE and Strive chipsets
- Introduction to OpenLANE detailed ASIC design flow

### SKY130_D1_SK3 — Get familiar to open-source EDA tools

- OpenLANE directory structure in detail
- Design Preparation Step
- Review files after design preparation and run synthesis
- OpenLANE project Git link description
- Steps to characterize synthesis results

## Conceptual Flow

```text
Software Application
        ↓
Compiler / Software Tools
        ↓
RTL Description
        ↓
Synthesis
        ↓
Gate-Level Netlist
        ↓
Floorplan
        ↓
Placement
        ↓
Clock Tree Synthesis
        ↓
Routing
        ↓
Sign-Off
        ↓
GDSII
```

OpenLANE is studied as the practical framework that connects these implementation stages. The Sky130 PDK supplies technology-specific information required by the tools.

## Practical Work

The module includes practical exposure to OpenLANE project organization, preparation of a design, synthesis execution, inspection of generated files and characterization of synthesis results. The figures below are embedded directly so that the README can be used as a visual workshop record without opening each image separately.

## Figures and Practical Evidence

### 1. Chip, Package, SoC and RISC-V Fundamentals

**Package and chip structure**

<img width="1552" height="868" alt="image" src="https://github.com/user-attachments/assets/b55bb2dc-e071-4972-b3a6-43bad3adc2bd" />

<img width="1548" height="862" alt="image" src="https://github.com/user-attachments/assets/26a45451-c307-4aff-8377-b6c1328cbaef" />

<img width="1286" height="772" alt="image" src="https://github.com/user-attachments/assets/1e8c1164-f34c-4416-9a3c-8faa005f4c7d" />

<img width="1712" height="843" alt="image" src="https://github.com/user-attachments/assets/8154cbaf-391f-4437-a72d-63ad4b8a8d15" />

<img width="1718" height="897" alt="image" src="https://github.com/user-attachments/assets/e120a110-7e1e-4c1a-afe4-22a99809bde7" />





### 2. Open-Source Digital ASIC Design and PDK
<img width="1743" height="947" alt="image" src="https://github.com/user-attachments/assets/45c33213-8034-4b98-993d-2a2a37e97cea" />

<img width="1711" height="876" alt="image" src="https://github.com/user-attachments/assets/3745297f-17bf-4123-a870-0a2f41bbcada" />

<img width="1285" height="356" alt="image" src="https://github.com/user-attachments/assets/6150c0ef-6c57-4b00-b134-a0f4946c7474" />

<img width="1273" height="767" alt="image" src="https://github.com/user-attachments/assets/09dec076-24c0-43b7-8de2-aa6f2670f77f" />




### 3. RTL-to-GDSII and OpenLANE Flow

<img width="1722" height="930" alt="image" src="https://github.com/user-attachments/assets/488d8bad-8c65-400f-935d-c00b3b8e27ee" />

<img width="1735" height="912" alt="image" src="https://github.com/user-attachments/assets/54c0bc5b-fbff-4a16-aec5-39472d47b22b" />

<img width="1725" height="883" alt="image" src="https://github.com/user-attachments/assets/e8680056-a7d5-4101-941c-142033f1554b" />

<img width="1687" height="882" alt="image" src="https://github.com/user-attachments/assets/cda3bf9d-87c8-4465-9507-1728e93bc389" />



### 4. Synthesis and Netlist

<img width="1891" height="1087" alt="image" src="https://github.com/user-attachments/assets/21066124-78f0-48a4-b401-79f4f542cd4c" />

<img width="1715" height="920" alt="image" src="https://github.com/user-attachments/assets/0fd6f61c-8778-4f66-be9c-fa6242a01796" />

<img width="1711" height="905" alt="image" src="https://github.com/user-attachments/assets/2b61455e-1cd5-419d-ad93-02b6ce764ec6" />

<img width="1917" height="1155" alt="image" src="https://github.com/user-attachments/assets/f40e514c-6892-4e56-932f-96e2e89db5d9" />



### 5. Physical Design Stages Introduced

<img width="1715" height="953" alt="image" src="https://github.com/user-attachments/assets/ad0410cf-e351-4c3c-b105-ce043354f5b0" />

<img width="1726" height="890" alt="image" src="https://github.com/user-attachments/assets/b3208100-612e-43db-bbfb-408bd550e7fe" />

<img width="1727" height="882" alt="image" src="https://github.com/user-attachments/assets/67460c30-dccb-4232-b8fd-5f676f703c10" />

<img width="1715" height="936" alt="image" src="https://github.com/user-attachments/assets/a8bdb6a7-fa4b-4089-9091-6d74a38adbb3" />

<img width="1721" height="981" alt="image" src="https://github.com/user-attachments/assets/6531ed14-a91f-4c27-8a81-65787918cf33" />

<img width="1583" height="833" alt="image" src="https://github.com/user-attachments/assets/f9e9293c-02c9-4ac3-a222-745aacbe6466" />

<img width="1696" height="905" alt="image" src="https://github.com/user-attachments/assets/aa655222-1ab1-4364-a605-93814505b4fd" />



### 6. Timing / Clock Information

<img width="1275" height="775" alt="image" src="https://github.com/user-attachments/assets/f5b21f7a-06b2-4d5a-ad11-ed0a08c1203e" />


## Important Concepts

### What is a PDK?

A Process Design Kit provides the technology-specific information required by EDA tools to design and implement a circuit for a particular semiconductor process. In this workshop, the Sky130 PDK is used as the technology context.

### What is Synthesis?

Synthesis converts an RTL description into a gate-level representation using available standard-cell libraries and design constraints. The resulting netlist becomes an input to subsequent physical implementation stages.

### Why OpenLANE?

The workshop uses OpenLANE to demonstrate an open-source digital ASIC implementation flow. It provides a practical environment in which synthesis and later physical-design stages can be executed using open-source tools and the Sky130 technology.

## Key Takeaways

- Digital IC implementation is a chain of connected stages rather than a single tool operation.
- The PDK establishes the technology context for the design tools.
- OpenLANE connects RTL design with physical implementation stages.
- Synthesis produces a gate-level netlist that is used by later physical-design stages.
- Understanding the flow and project structure is essential before performing floorplanning, placement, CTS and routing.

## Tools / Technologies Introduced

- OpenLANE
- Sky130 PDK
- Open-source EDA tools
- Linux / Ubuntu environment
- Synthesis and static-timing concepts
- RISC-V / SoC design context
