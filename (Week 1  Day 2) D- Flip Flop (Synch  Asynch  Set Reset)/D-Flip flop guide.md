# D Flip-Flop (DFF) — Complete Guide

This document (`dff.md`) provides a **complete reference** for designing, simulating, and synthesizing a **D Flip-Flop (DFF)** with **asynchronous set**, **asynchronous reset**, and **synchronous reset** concepts using Verilog. It covers Verilog RTL code, testbench, simulation with **Icarus Verilog (iverilog)**, waveform viewing with **GTKWave**, RTL synthesis with **Yosys**, and expected outputs.

---

## Table of Contents

* [Overview](#overview)
* [Prerequisites](#prerequisites)
* [Verilog RTL Code](#verilog-rtl-code)
* [Simulation with Icarus Verilog](#simulation-with-icarus-verilog)
* [Waveform Viewing in GTKWave](#waveform-viewing-in-gtkwave)
* [RTL Synthesis with Yosys](#rtl-synthesis-with-yosys)
* [Expected Output](#expected-output)

---

## Overview

A D Flip-Flop captures the value of the input `d` on the rising edge of the clock and presents it at output `q`. Enhancements:

* **Asynchronous Set (`asyncset`)**: Immediately forces `q = 1` regardless of clock.
* **Asynchronous Reset (`asynchreset`)**: Immediately forces `q = 0` regardless of clock.
* **Synchronous Reset (`sync_reset`)**: Resets `q = 0` only on the next clock edge when asserted.

---

## Prerequisites

* **Icarus Verilog** (`iverilog`)
* **GTKWave** (to view waveforms)
* **Yosys** (for RTL synthesis)
---

## Verilog RTL Code

```verilog

**ASynchronous set** 

module dff_async_set ( input clk ,  input async_set , input d , output reg q );
always @ (posedge clk , posedge async_set)
begin
	if(async_set)
		q <= 1'b1;
	else	
		q <= d;
end
endmodule

```
**Synchronous Reset**
```
module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk )
begin
	if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```
**ASynchronous Reset**
```
module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
	if(async_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```

**ASynchronous Reset and Synchronous Reset**
```
module dff_asyncres_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
	if(async_reset)
		q <= 1'b0;
	else if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```
---


## Simulation with Icarus Verilog
### Step 1: Clone the Workshop Repository

git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

cd sky130RTLDesignAndSynthesisWorkshop/verilog_files

### Step 2: Install Required Tools

sudo apt install iverilog

sudo apt install gtkwave

### Step 3: Simulate the Design

**Compile the design and testbench:** (file name vary as per type of d-FF)

iverilog asyncres.v tb_asyncres.v

**Run the simulation:**

./a.out

**View the waveform:** (file name vary as per type of d-FF)

gtkwave tb_asyncres.vcd

## RTL diagram generation with Yosys

### Step-by-Step Yosys Flow

**Start Yosys**

yosys

**Read the liberty library (Library file location can vary)**

read_liberty -lib /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib

**Read the Verilog code (file location can vary)**

read_verilog /home/vsduser/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/asyncres.v

**Synthesize the design**

synth -top asyncres

**Technology mapping (Library file location can vary)**

abc -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib 

**Visualize the gate-level netlist**

show

---

## Expected Output Waveform 


Synchronous Reset:

![synch reset dff output with code](https://github.com/user-attachments/assets/313ca01e-6edd-44ba-8514-8f06ae516c1c)

ASynchronous Reset:

![asynch reset dff output with code](https://github.com/user-attachments/assets/fad1e1f5-1536-441a-9268-b761351d7bb1)

ASynchronous set:

![asynch set dff output with code](https://github.com/user-attachments/assets/57de86e9-85f6-41c8-8f43-ff05839c0bc6)


ASynchronous Reset and Synchronous Reset:

![synch reset asynch reset dff output with code](https://github.com/user-attachments/assets/5d727fa8-6f7f-4a99-8a2f-c420c75f4542)



##RTL Diagram


Synchronous Reset:

![synch reset asynch reset dff RTL with code](https://github.com/user-attachments/assets/83b3f63c-2ec4-44fa-bfe4-b9e4aea6fb69)


ASynchronous Reset:
![asynch reset dff RTL with code](https://github.com/user-attachments/assets/fcbc3a01-58d8-40aa-a965-8fbfccad4dd4)


ASynchronous set:

![asynch set dff RTL with code](https://github.com/user-attachments/assets/d119535b-5084-4628-81ed-f12555d52cfa)

ASynchronous Reset and Synchronous Reset:

![synch reset asynch reset dff RTL with code](https://github.com/user-attachments/assets/4f16edac-b4aa-4c6d-b1f8-f1cacbb92eaf)



---
