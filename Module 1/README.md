# VSD RTL Design and Synthesis Workshop

## Workshop Overview

This workshop provides a practical introduction to **RTL (Register Transfer Level) Design** using **Verilog HDL**. The primary objective is to understand the complete RTL design flow, beginning with writing Verilog code, creating testbenches, simulating the design, and analyzing the generated waveforms.

During this workshop, I explored the complete digital design verification process using industry-standard open-source tools. I learned how to write Verilog modules, verify their functionality through simulation, and analyze timing waveforms before moving towards synthesis.

---

## What I Learned

Throughout this workshop, I learned to:

- Understand the RTL design flow.
- Write Verilog HDL modules for digital circuits.
- Create testbenches to verify RTL designs.
- Compile Verilog files using **Icarus Verilog**.
- Simulate digital circuits from the terminal.
- Generate Value Change Dump (VCD) files.
- Analyze simulation waveforms using **GTKWave**.
- Verify whether the RTL design functions as expected before synthesis.

---

## Definition

### Register Transfer Level (RTL)

**Register Transfer Level (RTL)** is a hardware abstraction level used to describe how digital data moves between registers and how logical operations are performed on that data using a Hardware Description Language such as Verilog.

### Testbench

A **Testbench** is a Verilog module used to apply different input combinations to the Design Under Test (DUT) and verify that the generated outputs match the expected functionality.

---

## Experiment

### Design

The design implemented in this experiment is a **2:1 Multiplexer** using Verilog HDL.

**Design File:** `good_mux.v`

**Testbench File:** `tb_good_mux.v`

---

## Commands Used

### Create the Design File

```bash
vim good_mux.v
```

### Create the Testbench File

```bash
vim tb_good_mux.v
```

### Compile the Design and Testbench

```bash
iverilog -o good_mux.out good_mux.v tb_good_mux.v
```

### Run the Simulation

```bash
./good_mux.out
```

### View the Waveform

```bash
gtkwave tb_good_mux.vcd
```

## RTL Design and Testbench

The screenshot below shows the Verilog design module and its corresponding testbench.

<img width="1164" height="882" alt="testbench" src="https://github.com/user-attachments/assets/4c50a09a-3c57-4d2c-88a0-828de890baa0" />


---

## Simulation Waveform

The following waveform confirms the correct functionality of the RTL design.

<img width="1910" height="916" alt="waveform" src="https://github.com/user-attachments/assets/15164d83-ea61-40ef-8fb6-dd0d1ee12604" />





---

## Observation

- Successfully compiled the Verilog files using Icarus Verilog.
- Simulated the RTL design using the generated executable.
- Generated the VCD file for waveform analysis.
- Verified the functionality of the design using GTKWave.
- Observed that the output changes correctly based on the applied inputs.

---

## Conclusion

This workshop helped me understand the complete RTL design and simulation flow using Verilog HDL. I learned how to write Verilog modules, create testbenches, compile and simulate designs using Icarus Verilog, generate VCD files, and analyze waveforms using GTKWave. Through this experiment, I gained practical experience in verifying digital circuit functionality before synthesis, which is an essential step in the VLSI design flow.

---

## Repository Structure

```
RTL_Design_Workshop/
│── README.md
│── good_mux.v
│── tb_good_mux.v
│── images/
│   ├── testbench.png
│   └── waveform.png
```

---
