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
* [Options & Flags](#options--flags)
* [Expected Output](#expected-output)
* [Troubleshooting](#troubleshooting)
* [License](#license)

---

## Overview

A 2:1 multiplexer selects one of two inputs (`a` or `b`) based on a select signal (`sel`). This design uses a **parameterized Verilog module** so you can easily change the bit-width. We will:

* Write RTL (`mux.v`)
* Write a testbench (`tb_mux.v`)
* Simulate using `iverilog` + `vvp`
* View waveforms in `gtkwave`
* Synthesize and generate RTL diagrams with `yosys`

---

## Prerequisites

* **Icarus Verilog** (`iverilog`, `vvp`)
* **GTKWave** (to view waveforms)
* **Yosys** (for RTL synthesis)
* **Graphviz** (optional, for DOT → PNG conversion)

Install (Ubuntu/Debian example):

```bash
sudo apt update
sudo apt install iverilog gtkwave yosys graphviz -y
```

---

## Verilog RTL Code

```verilog
// File: mux.v
// 2:1 Multiplexer
`timescale 1ns/1ps

module mux #(
    parameter WIDTH = 8
) (
    input  wire [WIDTH-1:0] a,
    input  wire [WIDTH-1:0] b,
    input  wire             sel,
    output wire [WIDTH-1:0] y
);
    assign y = sel ? b : a;
endmodule
```

---

## Testbench Code

```verilog
// File: tb_mux.v
`timescale 1ns/1ps

module tb_mux;
    parameter WIDTH = 8;
    reg [WIDTH-1:0] a;
    reg [WIDTH-1:0] b;
    reg sel;
    wire [WIDTH-1:0] y;

    mux #(.WIDTH(WIDTH)) dut (
        .a(a), .b(b), .sel(sel), .y(y)
    );

    initial begin
        $dumpfile("dump.vcd");
        $dumpvars(0, tb_mux);
    end

    initial begin
        a = 8'hAA; b = 8'h55; sel = 0;
        #5 sel = 1;
        #10 sel = 0;
        #5 a = 8'hFF; b = 8'h00;
        #5 sel = 1;
        #10 $finish;
    end

    initial begin
        $display("time\tsel\ta\tb\ty");
        $monitor("%0dns\t%b\t%h\t%h\t%h", $time, sel, a, b, y);
    end
endmodule
```

---

## Simulation with Icarus Verilog

```bash
# Compile
overilog -g2012 -o simv mux.v tb_mux.v

# Run simulation
vvp simv
```

This generates `dump.vcd` for waveform viewing.

---

## Waveform Viewing in GTKWave

Open the VCD file:

```bash
gtkwave dump.vcd
```

Drag `a`, `b`, `sel`, and `y` into the waveform viewer. You should see `y` follow `a` when `sel=0` and `b` when `sel=1`.

---

## RTL Synthesis with Yosys

### Method 1: Inline commands

```bash
yosys -p "read_verilog mux.v; prep -top mux; show"
```

### Method 2: Generate DOT + PNG

```bash
yosys -p "read_verilog mux.v; prep -top mux; write_dot mux.dot"
dot -Tpng mux.dot -o mux.png
```

This produces a block diagram of the MUX.

---

## Options & Flags

* **iverilog**: `-g2012` for SystemVerilog features
* **gtkwave**: `gtkwave tb_good_mux.vcd` to open waveform
* **yosys**: `show`, `write_dot` for visualization

---

## Expected Output
2. **Waveform**


3. **RTL Diagram**



## Troubleshooting

* If `dump.vcd` isn’t generated, check `$dumpfile` and `$dumpvars` in the testbench.
* Ensure Graphviz (`dot`) is installed if converting `.dot` → `.png`.
* Expand signals under `tb_mux` in GTKWave to plot them.

---

## License

MIT License — free to use and modify for learning or projects.

---
