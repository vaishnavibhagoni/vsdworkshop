# Module 4 — Pre-Layout Timing Analysis and Importance of Good Clock Tree

## Overview

Module 4 focuses on timing modelling and clock distribution. It begins with track information, standard-cell LEF generation, timing libraries and delay tables, then moves into timing analysis using OpenSTA. The module introduces setup time, hold time, clock jitter and uncertainty, followed by clock tree synthesis with TritonCTS.

The final part studies timing with real clocks and examines how clock-tree buffering and clock distribution affect setup and hold behavior.

## Learning Objectives

- Understand how layout/grid information is related to routing tracks.
- Understand the role of LEF and timing-library information in physical implementation.
- Explain delay tables and their use in timing modelling.
- Perform basic setup timing analysis using OpenSTA.
- Understand flip-flop setup and hold requirements.
- Understand clock jitter and uncertainty.
- Understand the purpose of clock tree synthesis.
- Explain clock buffering, H-tree distribution and clock-net shielding.
- Analyze setup and hold timing using real clocks.
- Understand the effect of CTS buffer sizing on timing.

## Topics Covered

### SKY130_D4_SK1 — Timing Modelling Using Delay Tables

- Lab steps to convert grid information to track information
- Lab steps to convert Magic layout to standard-cell LEF
- Introduction to timing libraries and steps to include a new cell in synthesis
- Introduction to delay tables
- Delay table usage Part 1
- Delay table usage Part 2
- Lab steps to configure synthesis settings to fix slack and include `vsdinv`

### SKY130_D4_SK2 — Timing Analysis with Ideal Clocks Using OpenSTA

- Setup timing analysis and introduction to flip-flop setup time
- Introduction to clock jitter and uncertainty
- Lab steps to configure OpenSTA for post-synthesis timing analysis
- Lab steps to optimize synthesis to reduce setup violations
- Lab steps to perform basic timing analysis

### SKY130_D4_SK3 — Clock Tree Synthesis, TritonCTS and Signal Integrity

- Clock tree routing and buffering using H-Tree algorithm
- Crosstalk and clock-net shielding
- Lab steps to run CTS using TritonCTS
- Lab steps to verify CTS results

### SKY130_D4_SK4 — Timing Analysis with Real Clocks Using OpenSTA

- Setup timing analysis using real clocks
- Hold timing analysis using real clocks
- Lab steps to analyze timing with real clocks using OpenSTA
- Lab steps to execute OpenSTA with correct timing libraries and CTS assignment
- Lab steps to observe the impact of bigger CTS buffers on setup and hold timing

## Timing Analysis Concepts

### Setup Time

Setup time is the required interval during which input data must be stable before the active clock edge of a sequential element. A setup violation indicates that data is not arriving with sufficient timing margin before the capture edge.

### Hold Time

Hold time is the required interval during which data must remain stable after the active clock edge. A hold violation indicates that data changes too soon after the capture edge.

### Clock Jitter and Uncertainty

Clock jitter represents variation in clock arrival timing. Clock uncertainty accounts for timing variations and margins used during analysis. Both influence the available timing budget.

### Delay Tables

Delay tables provide cell-delay information as a function of relevant operating conditions such as input transition and output load. They allow timing tools to estimate the behavior of library cells during analysis.

## Clock Tree Synthesis

```text
Clock Source
     ↓
Clock Distribution
     ↓
Buffering / H-Tree Structure
     ↓
Clock Sinks / Flip-Flops
```

CTS attempts to distribute the clock to sequential elements while controlling skew, delay and signal-integrity effects. The module also introduces shielding and crosstalk considerations for clock nets.

## Ideal Clock vs Real Clock

With an ideal clock, clock arrival is represented without the physical effects introduced by the clock network. After CTS, the real clock network has actual propagation and distribution characteristics, allowing setup and hold timing to be analyzed with a more physical clock model.

## Figures and Practical Evidence

### 1. Track, LEF and Timing-Library Preparation

<img width="1917" height="1140" alt="image" src="https://github.com/user-attachments/assets/3caea19c-6961-4e3e-9329-e5e49c323dd0" />

<img width="1917" height="781" alt="image" src="https://github.com/user-attachments/assets/e42665ad-a563-4814-9b7c-6a68f0490a03" />

<img width="1566" height="1010" alt="image" src="https://github.com/user-attachments/assets/e2345a66-4977-4b09-8af8-447a2cd74c26" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e97ecc5e-fb69-4ad8-b972-f0158ec7eb13" />



### 2. Delay Tables and SDC Constraints

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7df6f1fc-64b2-4a7e-a4d8-79a55e352956" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d049fb75-3676-4441-aba9-3d8a7ee0b610" />

### 3. OpenSTA Pre-Layout Timing Analysis

<img width="1917" height="1163" alt="image" src="https://github.com/user-attachments/assets/131e2720-11b0-42cf-a5d9-eb7bc1f59817" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c758b576-4e1c-463d-bf65-afff85426b63" />

### 4. Clock Tree Synthesis and Signal Integrity

<img width="1917" height="1092" alt="image" src="https://github.com/user-attachments/assets/72d19a5b-9703-4bde-846d-4eccf29d4e20" />


<img width="1917" height="1135" alt="image" src="https://github.com/user-attachments/assets/9f207443-2e1f-4eb7-8418-c987dc3c1d80" />
<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/ff33ea0c-d38a-40cc-9f42-15f67d4333eb" />


## Practical Interpretation

The timing workflow connects library data and SDC constraints to OpenSTA analysis. Timing reports can then be examined for critical paths, setup/hold behavior and available timing margin. CTS introduces the physical clock network, after which real-clock analysis can reveal effects that are not represented by an ideal clock.

## Key Takeaways

- Timing analysis depends on accurate cell and constraint information.
- Delay tables provide the cell timing behaviour used by timing analysis.
- OpenSTA can be used to examine timing paths and setup/hold conditions.
- Clock jitter and uncertainty reduce the available timing margin.
- CTS builds the clock network and uses buffering to distribute the clock.
- Crosstalk and shielding are important signal-integrity considerations for clock nets.
- Real-clock analysis includes the effects of the implemented clock network.

## Tools / Technologies

- OpenSTA
- TritonCTS
- Magic
- Sky130 timing libraries
- SDC constraints
- Standard-cell LEF / Liberty concepts
