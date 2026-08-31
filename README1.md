# vsdworkshop

## 1. Introduction

RTL (Register Transfer Level) design describes the digital circuit using a hardware description language such as Verilog.

The complete flow used in this workshop is:

**RTL Design → Functional Simulation → Synthesis → Gate-Level Netlist → Gate-Level Simulation (GLS)**

For the BabySoC design, the flow is:

**RTL → Pre-Synthesis Simulation → Yosys Synthesis → Gate-Level Netlist → Post-Synthesis Simulation**

---

# 2. Tools Used

The following tools are used:

- **Icarus Verilog (iverilog)** – Verilog simulation
- **GTKWave** – Waveform viewing
- **Yosys** – RTL synthesis
- **Sky130 Liberty files** – Standard-cell timing/library information
- **Sky130 Verilog models** – Gate-level simulation models
- **VSDBabySoC** – SoC design used for synthesis and simulation

---


# 3. Tool Installation and Setup

Update the package information:

`sudo apt-get update`

Install Icarus Verilog:

`sudo apt-get install iverilog`

Check Yosys:

`yosys`

GTKWave can be launched using:

`gtkwave`

These tools are used for RTL simulation, waveform analysis, and synthesis.

---
# Good MUX RTL Design

## Introduction

A **Multiplexer (MUX)** is a combinational digital circuit that selects one input from multiple inputs and sends the selected input to the output.

A **2:1 MUX** has:

- Two data inputs: `i0` and `i1`
- One select line: `sel`
- One output: `y`

The select line determines which input is connected to the output.

### Truth Table

| Select (`sel`) | Output (`y`) |
|---|---|
| 0 | `i0` |
| 1 | `i1` |

The Boolean expression for a 2:1 MUX is:

`y = (~sel & i0) | (sel & i1)`

---

# RTL Design

The MUX is described using **Verilog HDL** at the RTL level.

### Command

`vi good_mux.v`

### Good MUX RTL Code

verilog
module good_mux (
    input i0,
    input i1,
    input sel,
    output y
);

assign y = sel ? i1 : i0;

endmodule
### RTL Screenshot

*Add the Good MUX RTL screenshot here.*

---

# 3. Testbench

A **testbench** is used to apply different input combinations to the MUX and verify its output.

The testbench file is:

`tb_good_mux.v`

The testbench checks both select conditions:

**sel = 0 → y = i0**

**sel = 1 → y = i1**

### Testbench Screenshot


<img width="1060" height="840" alt="test_goodmux" src="https://github.com/user-attachments/assets/1c0088dd-bece-415b-ba49-0774d5efbb8d" />



---

# 4. Functional Simulation

Functional simulation verifies the behavior of the RTL design before synthesis.

### Compile the RTL and Testbench

`iverilog good_mux.v tb_good_mux.v`

### Run the Simulation

`./a.out`

The simulation generates a VCD waveform file.

### View the Waveform

`gtkwave tb_good_mux.vcd`



### RTL Simulation Waveform


<img width="1600" height="859" alt="simlution" src="https://github.com/user-attachments/assets/1e39b18a-ddd3-4a84-ac2e-25553decf818" />


The waveform verifies that the output follows the selected input correctly.
# 4. RTL Design

**RTL (Register Transfer Level)** is the Verilog description of the hardware design before synthesis.

The main VSDBabySoC RTL file is:

`vsdbabysoc.v`

Supporting RTL files include modules such as:

`clk_gate.v`

Other Verilog source files are used by the VSDBabySoC design depending on the project configuration.

To locate the RTL files:

`find . -name "*.v"`

To open the main RTL file:

`gvim vsdbabysoc.v`

To view the RTL contents:

`cat vsdbabysoc.v`

or:

`more vsdbabysoc.v`

The RTL describes the intended functionality and hardware structure of the VSDBabySoC before synthesis.
# 5. Functional / RTL Simulation

## Theory

Functional simulation checks whether the **VSDBabySoC RTL design** behaves correctly according to its intended functionality.

At this stage:

- The design is still in RTL form.
- No synthesized standard-cell gates are involved.
- The testbench provides the required input and clock signals.
- Icarus Verilog performs the simulation.
- The simulator generates a VCD waveform file.
- GTKWave is used to observe the waveform.

## Simulation Flow

**VSDBabySoC RTL**  
↓  
**Testbench**  
↓  
**Icarus Verilog**  
↓  
**VCD File**  
↓  
**GTKWave**

## Commands

Navigate to the required project directory and check the files:

`pwd`

`ls`

Compile the RTL and testbench using Icarus Verilog:

`iverilog -o vsdbabysoc_sim vsdbabysoc.v <testbench_file>.v`

Run the simulation:

`vvp vsdbabysoc_sim`

Check the generated files:

`ls`

Check for the generated VCD file:

`ls *.vcd`

Open the generated waveform:

`gtkwave dump.vcd`

The waveform can be used to verify the functional behavior of the VSDBabySoC RTL before synthesis.

<img width="720" height="1280" alt="yosys" src="https://github.com/user-attachments/assets/430d3d5e-c803-4363-96f0-c5c450d1d0cf" />


# 6. Synthesis

## Theory

**Synthesis** converts the RTL description into a gate-level representation using available standard cells.

The basic synthesis process is:

**RTL → Logic Optimization → Standard Cells → Gate-Level Netlist**

For the VSDBabySoC design, **Yosys** is used for RTL synthesis.

The synthesis process analyzes the Verilog RTL and maps the required logic to cells available in the target technology library.

## Sky130 Standard-Cell Library

The Sky130 technology library provides information about the available standard cells, including their functionality, timing, and electrical characteristics.

An example Sky130 Liberty file is:

`sky130_fd_sc_hd__tt_025C_1v80.lib`

Here:

- `sky130` refers to the SkyWater 130 nm technology.
- `fd_sc_hd` refers to the standard-cell library and high-density library variant.
- `tt` represents the typical process corner.
- `025C` represents the temperature condition.
- `1v80` represents the nominal supply voltage.

## Synthesis Flow

**VSDBabySoC RTL**  
↓  
**Yosys**  
↓  
**Logic Synthesis**  
↓  
**Technology Mapping**  
↓  
**Gate-Level Netlist**

## Start Yosys

`yosys`

## Read the RTL

Inside Yosys, the RTL is read using:

`read_verilog ./module/vsdbabysoc.v`

## Prepare the Design

`prep -top vsdbabysoc`

This prepares the design for synthesis and identifies `vsdbabysoc` as the top-level module.

## Perform Synthesis

`synth`

Yosys synthesizes and optimizes the RTL design.

## Display Synthesis Statistics

`stat`

This displays information about the synthesized design, including wires, cells, and logic elements.

## Generate the Synthesized Netlist

`write_verilog synthesized_netlist.v`

This generates the gate-level Verilog netlist.

## Exit Yosys

`exit`

## Yosys Synthesis Output



<img width="720" height="1080" alt="yosys" src="https://github.com/user-attachments/assets/98952223-f3c7-44fa-8e21-28d528fefd6e" />

# 8. Read the Standard-Cell Library

For synthesis and technology mapping, the Sky130 standard-cell Liberty file is used.

The Liberty file contains information about standard cells such as:

- Logic functions
- Timing characteristics
- Area information
- Input and output properties

The Sky130 Liberty file used in the BabySoC flow is:

`sky130_fd_sc_hd__tt_025C_1v80.lib`

Load the library in Yosys using:

`read_liberty -lib src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

---

# 9. Read the VSDBabySoC RTL

The main BabySoC RTL module is:

`vsdbabysoc.v`

The supporting RTL includes:

- `rvmyth.v`
- `clk_gate.v`

The RTL files are read into Yosys before synthesis.

For example:

`read_verilog src/module/vsdbabysoc.v`

`read_verilog -I src/include src/module/rvmyth.v`

`read_verilog -I src/include src/module/clk_gate.v`

---

# 10. RTL Synthesis

The top-level module of the VSDBabySoC design is:

`vsdbabysoc`

The synthesis command is:

`synth -top vsdbabysoc`

The `synth` command converts the RTL description into a synthesized logic representation.

The basic flow is:

**VSDBabySoC RTL**  
↓  
**Yosys Synthesis**  
↓  
**Synthesized Logic**

---

# 11. Technology Mapping

Technology mapping maps the synthesized logic to cells available in the selected Sky130 standard-cell library.

The DFF cells are mapped using:

`dfflibmap -liberty src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

Logic optimization and technology mapping can then be performed using ABC:

`abc -liberty src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

The result is a technology-mapped gate-level design using Sky130 standard cells.

---

# 12. View the Synthesized Design

Yosys can display the synthesized logic structure using:

`show`

This displays the synthesized design structure generated by Yosys.

<img width="3840" height="2160" alt="pre" src="https://github.com/user-attachments/assets/aab67824-9b62-4a86-ae19-64c0a0e8011f" />


---

# 13. Generate the Gate-Level Netlist

After synthesis and technology mapping, the synthesized design can be exported as a Verilog netlist.

Use:

`write_verilog -noattr vsdbabysoc_netlist.v`

The generated file:

`vsdbabysoc_netlist.v`

contains the synthesized gate-level representation of the BabySoC.

The basic transformation is:

**vsdbabysoc.v**  
↓  
**Yosys**  
↓  
**vsdbabysoc_netlist.v**

The original file represents the RTL, while the generated file represents the synthesized gate-level implementation.

---

# 14. Gate-Level Simulation (GLS)

## Theory

**Gate-Level Simulation (GLS)** verifies the behavior of the synthesized gate-level netlist.

Instead of simulating only the original RTL, GLS simulates:

**Gate-Level Netlist + Standard-Cell Models + Testbench**

This verifies that the synthesized implementation preserves the intended functionality of the original RTL.

---

# 15. Sky130 Verilog Models

The synthesized netlist contains Sky130 standard-cell instances.

Therefore, the corresponding Sky130 Verilog cell models are required for gate-level simulation.

The standard-cell Verilog models are located in the project library/model directory.

Typical model files include:

- `primitives.v`
- `sky130_fd_sc_hd.v`

These files provide Verilog simulation models for the Sky130 standard cells used in the synthesized netlist.

---

# 16. Post-Synthesis / Gate-Level Simulation

The synthesized BabySoC netlist is simulated using the testbench together with the required standard-cell models.

The GLS flow is:

**Synthesized Netlist**  
↓  
**Sky130 Verilog Models**  
↓  
**Testbench**  
↓  
**Icarus Verilog**  
↓  
**GLS VCD**  
↓  
**GTKWave**

The exact compilation command depends on the generated netlist and the location of the standard-cell model files.

---

# 17. VSDBabySoC

## Theory

**VSDBabySoC** is a small System-on-Chip design used to demonstrate the RTL-to-netlist design flow.

The design contains important modules such as:

- `vsdbabysoc.v`
- `rvmyth.v`
- `clk_gate.v`

The design also uses supporting libraries such as:

- `avsdpll.lib`
- `avsddac.lib`
- Sky130 standard-cell Liberty files

The overall BabySoC flow is:

**RTL**  
↓  
**Pre-Synthesis Simulation**  
↓  
**Yosys Synthesis**  
↓  
**Gate-Level Netlist**  
↓  
**Post-Synthesis Simulation**

---

# 18. Pre-Synthesis Simulation

## Theory

Pre-synthesis simulation is the simulation of the original BabySoC RTL before synthesis.

It verifies the functional behavior of the complete RTL design using the testbench.

From the VSDBabySoC project directory, the simulation can be compiled using:

`iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/`

Here:

- `-o ./pre_synth_sim.out` creates the simulation executable.
- `-DPRE_SYNTH_SIM` enables the pre-synthesis simulation configuration.
- `-I src/include` specifies the include directory.
- `-I src/module/` specifies the RTL module directory.

Run the simulation using:

`./pre_synth_sim.out`

The simulation generates the waveform file specified by the testbench.

The waveform can then be opened using GTKWave:

`gtkwave <generated_vcd_file>.vcd`

## Pre-Synthesis Waveform

<img width="3840" height="2160" alt="pre" src="https://github.com/user-attachments/assets/89e7f996-5ad8-49f5-aaaa-5fc73a5dddf8" />


---

# 19. BabySoC RTL Synthesis

The VSDBabySoC synthesis flow is controlled using a Yosys synthesis script.

Move to the script directory:

`cd /home/vsduser/VSDBabySoC/src/script`

Check the available files:

`ls`

The synthesis script is:

`yosys.ys`

Open the script using:

`gvim yosys.ys`

The script contains the commands required to read the RTL, load the required libraries, synthesize the design, perform technology mapping, and generate the synthesized netlist.

---

# 20. Read BabySoC Libraries

The BabySoC design uses analog and standard-cell library information.

Read the PLL library:

`read_liberty -lib src/lib/avsdpll.lib`

Read the DAC library:

`read_liberty -lib src/lib/avsddac.lib`

Read the Sky130 standard-cell library:

`read_liberty -lib src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

These libraries provide information required by the synthesis and technology-mapping process.

---

# 21. Read BabySoC RTL

Read the main BabySoC RTL:

`read_verilog src/module/vsdbabysoc.v`

Read the RVMYTH processor RTL:

`read_verilog -I src/include src/module/rvmyth.v`

Read the clock-gating RTL:

`read_verilog -I src/include src/module/clk_gate.v`

These files together describe important parts of the VSDBabySoC design.

---

# 22. Synthesize BabySoC

Specify the top-level module:

`synth -top vsdbabysoc`

The top-level module is:

`vsdbabysoc`

Yosys synthesizes the RTL into a logic-level representation.

---

# 23. DFF Technology Mapping

The synthesized flip-flops are mapped to available Sky130 standard-cell flip-flops using:

`dfflibmap -liberty src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

This maps generic flip-flops to technology-specific standard cells.

---

# 24. Optimization

Optimize the synthesized design:

`opt`

Optimization removes unnecessary logic and simplifies the synthesized design.

---

# 25. Technology Mapping Using ABC

Perform technology mapping using the Sky130 standard-cell library:

`abc -liberty src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

This maps the synthesized logic to available Sky130 standard cells.

---

# 26. View BabySoC Schematic

To view the synthesized BabySoC design:

`show vsdbabysoc`

This displays the synthesized design structure.

_Add the Yosys schematic screenshot here._

---

# 27. Flatten the Design

Flatten the hierarchical design:

`flatten`

Flattening removes the module hierarchy and combines the design into a single representation.

---

# 28. Handle Undefined Values

Set undefined values to zero:

`setundef -zero`

This replaces undefined values with zero where required.

---

# 29. Clean the Design

Remove unused or unnecessary elements:

`clean -purge`

This removes unused wires, cells, and logic from the design.

---

# 30. Rename Generated Objects

Rename generated objects:

`rename -enumerate`

This gives unique enumerated names to generated objects.

---

# 31. Generate BabySoC Netlist

Export the synthesized BabySoC netlist:

`write_verilog -noattr baby_soc_netlist3.v`

The generated file is:

`baby_soc_netlist3.v`

This file contains the gate-level representation of the synthesized BabySoC.

The transformation is:

**VSDBabySoC RTL**  
↓  
**Yosys Synthesis**  
↓  
**Optimization**  
↓  
**Technology Mapping**  
↓  
**Gate-Level Netlist**

---

# 32. Post-Synthesis Simulation

## Theory

Post-synthesis simulation verifies the synthesized BabySoC netlist using the functional testbench.

The main difference is:

**Pre-Synthesis:**  
RTL modules + testbench

**Post-Synthesis:**  
Gate-level netlist + standard-cell models + testbench

This allows us to check whether the synthesized implementation preserves the intended RTL behavior.

---

# 33. Compile Post-Synthesis Simulation

The post-synthesis simulation is compiled using Icarus Verilog.

A typical command used in the flow is:

`sudo iverilog -o /post_synth_sim.out -DPOST_SYNTH_SIM -I src/include/ -I ../../sky130RTLDesignAndSynthesisWorkshop/my_lib/verilog_model/ -I src/module/ src/module/testbench.v`

Another form used during the flow is:

`sudo iverilog -DPOST_SYNTH_SIM -I src/include/ -I ../../sky130RTLDesignAndSynthesisWorkshop/my_lib/verilog_model/ -I src/module/ src/module/testbench.v`

The important option is:

`-DPOST_SYNTH_SIM`

This tells the testbench to use the post-synthesis simulation configuration.

The include paths provide access to:

- `src/include/`
- `my_lib/verilog_model/`
- `src/module/`

The standard-cell Verilog models are required because the synthesized netlist contains technology-specific Sky130 cells.

---

# 34. Run the Post-Synthesis Simulation

If the simulation executable was generated as `a.out`, run:

`./a.out`

If the output file was explicitly created as `post_synth_sim.out`, run:

`./post_synth_sim.out`

The testbench executes the synthesized BabySoC gate-level netlist.

---

# 35. View the Post-Synthesis Waveform

Check the generated VCD file:

`ls *.vcd`

Open the VCD file using GTKWave.

For example:

`gtkwave post_synth_sim.vcd`

Use the actual VCD filename generated by the testbench if it is different.

The post-synthesis waveform can then be compared with the pre-synthesis RTL waveform.

## Post-Synthesis / GLS Waveform


<img width="1600" height="847" alt="post" src="https://github.com/user-attachments/assets/f8051bf1-4a78-4855-838c-a0ba1173e143" />


---

# 36. Complete BabySoC Flow

The complete flow can be represented as:

**VSDBabySoC RTL**  
↓  
**Pre-Synthesis Simulation**  
↓  
**Yosys**  
↓  
**RTL Synthesis**  
↓  
**Optimization**  
↓  
**DFF Mapping**  
↓  
**ABC Technology Mapping**  
↓  
**Gate-Level Netlist**  
↓  
**Post-Synthesis Simulation**  
↓  
**GTKWave**

---

# 37. Important Concepts

### RTL

RTL describes the intended hardware behavior using Verilog.

### Simulation

Simulation verifies the behavior of the design before hardware implementation.

### Synthesis

Synthesis converts RTL into a gate-level representation.

### Technology Mapping

Technology mapping converts generic synthesized logic into cells available in a specific technology library such as Sky130.

### Netlist

A netlist is a structural description of the circuit containing cells, gates, and their connections.

### Pre-Synthesis Simulation

Simulation performed on the original RTL before synthesis.

### Post-Synthesis Simulation

Simulation performed on the synthesized gate-level netlist.

### GLS

GLS stands for **Gate-Level Simulation**. It verifies the behavior of the synthesized gate-level implementation.

### Liberty File

A `.lib` file contains information about standard cells, including their functionality, timing, area, and electrical characteristics.

### Verilog Cell Models

Files such as:

`primitives.v`

`sky130_fd_sc_hd.v`

provide Verilog models required to simulate Sky130 standard cells.

---

# 38. Final RTL-to-GLS Flow

The complete RTL-to-GLS flow used in this workshop is:

**1. Write RTL**  
↓  
**2. Write Testbench**  
↓  
**3. Functional / RTL Simulation**  
↓  
**4. Pre-Synthesis Simulation**  
↓  
**5. Read RTL into Yosys**  
↓  
**6. Read Liberty Libraries**  
↓  
**7. Synthesize**  
↓  
**8. Optimize**  
↓  
**9. DFF Mapping**  
↓  
**10. ABC Technology Mapping**  
↓  
**11. Generate Gate-Level Netlist**  
↓  
**12. Post-Synthesis / GLS**  
↓  
**13. View Waveform in GTKWave**  
↓  
**14. Compare RTL and GLS Results**

---

# 39. Conclusion

The RTL-to-Gate-Level flow demonstrates how the VSDBabySoC Verilog design is transformed into a technology-mapped gate-level implementation.

Pre-synthesis simulation verifies the functionality of the original RTL, while synthesis converts the RTL into a gate-level netlist using the Sky130 standard-cell library.

Post-synthesis or Gate-Level Simulation then verifies the synthesized implementation using the required standard-cell models and testbench.

Comparing the RTL and GLS waveforms helps confirm that the synthesized BabySoC preserves the intended functional behavior.
