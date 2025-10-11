#  Part 3 – Generate Timing Graphs with OpenSTA

---

##  Objectives

1. Perform **Gate-Level Simulation (GLS)** and validate **functional correctness** post-synthesis.  
2. Gain basic **Static Timing Analysis (STA)** knowledge.  
3. Generate **timing graphs using OpenSTA** and interpret **timing paths**.

---

##  About OpenSTA

**OpenSTA** is an open-source **Static Timing Analysis (STA)** tool developed under the **OpenROAD Project**.  
It helps engineers verify and analyze the timing performance of synthesized netlists, ensuring designs meet setup and hold time constraints.

-  **GitHub:** [The OpenROAD Project / OpenSTA](https://github.com/The-OpenROAD-Project/OpenSTA)
-  **Documentation:** [OpenSTA User Guide (PDF)](https://github.com/The-OpenROAD-Project/OpenSTA/blob/master/doc/OpenSTA.pdf)
-  **Example Script (Day 19 Reference):** [VSD HDP Workshop Example](https://github.com/arunkpv/vsd-hdp/blob/main/docs/Day_19.md)

---

##  Steps to Perform Timing Analysis Using OpenSTA

Follow these steps to load your synthesized design, perform STA, and generate timing graphs.

### 1. Load Synthesized Netlist and Libraries
Load the technology library and synthesized gate-level netlist:

```tcl

read_liberty /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog /path/to/vsdbabysoc.synth.v

```

### 2. Load Timing Constraints

Provide clock and I/O timing information:
```
read_sdc /path/to/constraints.sdc
```

### 3. Link the Design
Link all design components for timing analysis:
```
link_design vsdbabysoc
```

### 6. Generate Timing Reports

Run STA to analyze setup and hold timing checks:
```
report_checks -path full -fields {slew cap delay time slack} -digits 3 > timing_report.txt
report_tns
report_wns
```
### 5. Generate and Export Timing Graphs

Visualize timing paths and export timing data:
```
report_timing -max_paths 10 -delay max
report_timing -max_paths 10 -delay min
```

Optional – export a graph view of timing paths:
```
write_dot_timing_graph timing_graph.dot
```
You can view .dot files using Graphviz or any online DOT graph viewer.
```
read_liberty /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog /path/to/vsdbabysoc.synth.v
