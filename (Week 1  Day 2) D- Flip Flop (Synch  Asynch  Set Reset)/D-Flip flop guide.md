# D Flip-Flop (DFF) — Complete Guide

This document (`dff.md`) provides a **complete reference** for designing, simulating, and synthesizing a **D Flip-Flop (DFF)** with **asynchronous set**, **asynchronous reset**, and **synchronous reset** concepts using Verilog. It covers Verilog RTL code, testbench, simulation with **Icarus Verilog (iverilog)**, waveform viewing with **GTKWave**, RTL synthesis with **Yosys**, and expected outputs.

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

A D Flip-Flop captures the value of the input `d` on the rising edge of the clock and presents it at output `q`. Enhancements:

* **Asynchronous Set (`asyncset`)**: Immediately forces `q = 1` regardless of clock.
* **Asynchronous Reset (`asynchreset`)**: Immediately forces `q = 0` regardless of clock.
* **Synchronous Reset (`sync_reset`)**: Resets `q = 0` only on the next clock edge when asserted.

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
// File: dff.v
`timescale 1ns/1ps

module dff (
    input  wire clk,
    input  wire d,
    input  wire arst,   // asynchronous reset (active high)
    input  wire set,    // asynchronous set (active high)
    input  wire srst,   // synchronous reset (active high)
    output reg  q
);

    always @(posedge clk or posedge arst or posedge set) begin
        if (arst)
            q <= 1'b0;     // async reset
        else if (set)
            q <= 1'b1;     // async set
        else if (srst)
            q <= 1'b0;     // sync reset
        else
            q <= d;        // normal operation
    end

endmodule
```

---

## Testbench Code

```verilog
// File: tb_dff.v
`timescale 1ns/1ps

module tb_dff;

    reg clk;
    reg d;
    reg arst;
    reg set;
    reg srst;
    wire q;

    // Instantiate DFF
    dff uut (
        .clk(clk),
        .d(d),
        .arst(arst),
        .set(set),
        .srst(srst),
        .q(q)
    );

    initial begin
        $dumpfile("tb_dff.vcd");
        $dumpvars(0, tb_dff);
    end

    // Clock generation
    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end

    // Stimulus
    initial begin
        d = 0; arst = 0; set = 0; srst = 0;

        #10 d = 1;              // normal operation
        #10 arst = 1;           // async reset
        #10 arst = 0; d = 0;
        #10 set = 1;            // async set
        #10 set = 0; d = 1;
        #10 srst = 1;           // sync reset
        #10 srst = 0; d = 1;
        #20 $finish;
    end

    initial begin
        $display("time\tclk\td\tarst\tset\tsrst\tq");
        $monitor("%0dns\t%b\t%b\t%b\t%b\t%b\t%b", $time, clk, d, arst, set, srst, q);
    end

endmodule
```

---

## Simulation with Icarus Verilog

```bash
# Compile
overilog -g2012 -o simv dff.v tb_dff.v

```

This generates `tb_dff.vcd` for waveform viewing.

---

## Waveform Viewing in GTKWave

```bash
gtkwave tb_dff.vcd
```

* Observe `q` following `d` on the clock edges.
* When **`arst=1`**, `q` → 0 immediately.
* When **`set=1`**, `q` → 1 immediately.
* When **`srst=1`**, `q` resets to 0 on the **next clock edge**.

---

## RTL Synthesis with Yosys

```bash
yosys -p "read_verilog dff.v; prep -top dff; show"
```

Or generate a diagram file:

```bash
yosys -p "read_verilog dff.v; prep -top dff; write_dot dff.dot"
dot -Tpng dff.dot -o dff.png
```

---

## Expected Output

```

**Waveform:**

**Synchronous Reset:**

**ASynchronous Reset:**

**ASynchronous set:**

**ASynchronous Reset and Synchronous Reset:**




**RTL Diagram:**


**Synchronous Reset:**

**ASynchronous Reset:**

**ASynchronous set:**

**ASynchronous Reset and Synchronous Reset:**



---
