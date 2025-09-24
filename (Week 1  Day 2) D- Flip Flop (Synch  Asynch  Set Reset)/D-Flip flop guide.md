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

**Compile the design and testbench:**

iverilog good_mux.v tb_good_mux.v

**Run the simulation:**

./a.out

**View the waveform:**

gtkwave tb_good_mux.vcd

## RTL diagram generation with Yosys

### Step-by-Step Yosys Flow

**Start Yosys**

yosys

**Read the liberty library (Library file loaction can vary)**

read_liberty -lib /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib

**Read the Verilog code (file loaction can vary)**

read_verilog /home/vsduser/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/good_mux.v

**Synthesize the design**

synth -top good_mux

**Technology mapping (Library file loaction can vary)**

abc -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib 

**Visualize the gate-level netlist**

show

---

## Expected Output

```

**Waveform:**

**Synchronous Reset:**
![synch reset dff output with code](https://github.com/user-attachments/assets/071b97a9-d54b-4877-ab27-d053dd1a54a1)

**ASynchronous Reset:**

![asynch reset dff output with code](https://github.com/user-attachments/assets/a9c4084b-5c59-41f6-96ec-440ee0fae174)

**ASynchronous set:**
![asynch set dff output with code](https://github.com/user-attachments/assets/36e94fbb-ffd8-4963-bd8c-f58c39e91f93)


**ASynchronous Reset and Synchronous Reset:**


![synch reset asynch reset dff output with code](https://github.com/user-attachments/assets/9a8a392d-ba1f-4c26-8194-082561128ebf)


**RTL Diagram:**


**Synchronous Reset:**
![synch reset dff RTL with code](https://github.com/user-attachments/assets/b17e6e6c-cfa9-4f35-8740-441a184646f7)


**ASynchronous Reset:**
![asynch reset dff RTL with code](https://github.com/user-attachments/assets/45c16813-fb1a-44b9-8467-56d9cf17d34a)


**ASynchronous set:**

![asynch set dff RTL with code](https://github.com/user-attachments/assets/4eee5936-4893-4f40-bbea-093b93b17403)

**ASynchronous Reset and Synchronous Reset:**

![synch reset asynch reset dff RTL with code](https://github.com/user-attachments/assets/0b80f99b-f332-43d7-aa39-de427601974e)

---
