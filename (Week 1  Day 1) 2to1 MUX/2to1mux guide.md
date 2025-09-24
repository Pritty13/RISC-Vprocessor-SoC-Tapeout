# 2-to-1 Multiplexer (MUX) — Complete Guide

This document (`2to1mux.md`) provides a **complete reference** for designing, simulating, and synthesizing a **2:1 multiplexer** using Verilog. It covers Verilog RTL code, testbench, simulation with **Icarus Verilog (iverilog)**, waveform viewing with **GTKWave**, RTL synthesis with **Yosys**, and options for generating RTL diagrams.

---

## Table of Contents

* [Overview](#overview)
* [Prerequisites](#prerequisites)
* [Verilog RTL Code](#verilog-rtl-code)
* [Testbench Code](#testbench-code)
* [Simulation with Icarus Verilog](#simulation-with-icarus-verilog)
* [Waveform Viewing in GTKWave](#waveform-viewing-in-gtkwave)
* [RTL Synthesis with Yosys](#rtl-synthesis-with-yosys)
* [Expected Output](#expected-output)


---

## Overview

A 2:1 multiplexer selects one of two inputs (`a` or `b`) based on a select signal (`sel`). This design uses a **parameterized Verilog module** so you can easily change the bit-width. We will:

* Write RTL (`good_mux.v`)
* Write a testbench (`tb_good_mux.v`)
* Simulate using `iverilog`
* View waveforms in `gtkwave`
* Synthesize and generate RTL diagrams with `yosys`

---

## Prerequisites

* **Icarus Verilog** (`iverilog`)
* **GTKWave** (to view waveforms)
* **Yosys** (for RTL synthesis)

Install (Ubuntu/Debian example):

```bash
sudo apt update
sudo apt install iverilog gtkwave yosys graphviz -y
```

---

## Verilog RTL Code

```verilog
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```

---

## Testbench Code

```verilog
// File: tb_good_mux.v

```
```

---

`timescale 1ns / 1ps

module tb_good_mux;

	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;

always #10 i0 = ~i0;

always #55 i1 = ~i1;

endmodule
```

---

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

**Read the liberty library (Library file location can vary)**

read_liberty -lib /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib

**Read the Verilog code (file location can vary)**

read_verilog /home/vsduser/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/good_mux.v

**Synthesize the design**

synth -top good_mux

**Technology mapping (Library file location can vary)**

abc -liberty /address/to/your/sky130/file/sky130_fd_sc_hd__tt_025C_1v80.lib 

**Visualize the gate-level netlist**

show


## Expected Output
 **Waveform**

![mux 2to1 iverilog gtkwave output with code](https://github.com/user-attachments/assets/d03b90d7-ff19-402f-9d4b-71e274cd6501)

 **RTL Diagram**

![mux 2to1 iverilog yosys RTL with code](https://github.com/user-attachments/assets/36987b49-f3e6-4626-92b5-3d16545c537e)



