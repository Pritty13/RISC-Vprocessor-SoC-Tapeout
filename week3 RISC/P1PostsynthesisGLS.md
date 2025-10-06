# BabySoC Gate-Level Simulation (GLS) – Post-Synthesis

---

## Purpose of GLS

Gate-Level Simulation (GLS) is used to **verify the functionality of a design after the synthesis process**. Unlike behavioral or RTL (Register Transfer Level) simulations, which operate at a higher abstraction level, GLS works on the **netlist generated post-synthesis**, which includes the actual gates and interconnections used to implement the design.

---

## Key Aspects of GLS for BabySoC

### 1. Verification with Timing Information
- GLS is performed using **Standard Delay Format (SDF) files** to ensure timing correctness.
- Ensures that the SoC behaves correctly under **real-world timing constraints**.

### 2. Design Validation Post-Synthesis
- Confirms that the design's **logical behavior** remains correct after mapping it to the gate-level representation.
- Ensures the design is free from issues like **metastability or glitches**.

### 3. Simulation Tools
- Tools like **Icarus Verilog** (iverilog) or similar simulators are used to compile and run the gate-level netlist.
- Waveforms are typically analyzed using **GTKWave**.

### 4. Importance for BabySoC
- BabySoC consists of multiple modules like the **RISC-V processor, PLL, and DAC**.
- GLS ensures these modules **interact correctly** and meet **timing requirements** in the synthesized design.

---

## Step-by-Step Execution Plan

### 1. Load the Top-Level Design and Supporting Modules in Yosys

```tcl
yosys
```


### 2. Read top-level RTL and modules
```
read_verilog /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/module/vsdbabysoc.v
read_verilog -I /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/module/rvmyth.v
read_verilog -I /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/module/clk_gate.v
```
### 3. Read standard cell and IP libraries
```
read_liberty -lib /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/avsdpll.lib
read_liberty -lib /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/avsddac.lib
read_liberty -lib /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
### 4. Synthesize the top-level design
```
synth -top vsdbabysoc
```
### 5. Map D flip-flops to library
```
dfflibmap -liberty /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
### 6. Technology mapping and optimization
```
abc -liberty /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib \
    -script +strash;scorr;ifraig;retime;{D};strash;dch,-f;map,-M,1,{D}
```
### 7. Flatten hierarchy and clean design
```
flatten
setundef -zero
clean -purge
rename -enumerate
```
### 8. Get design statistics
```
stat
```
### 9. Write post-synthesis Verilog netlist
```
write_verilog -noattr /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/output/post_synth_sim/vsdbabysoc.synth.v

```
# POST_SYNTHESIS SIMULATION AND WAVEFORMS
## 1.  Compile the Gate-Level Netlist with Icarus Verilog
```
iverilog -o /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/output/post_synth_sim/post_synth_sim.out -DPOST_SYNTH_SIM -DFUNCTIONAL -DUNIT_DELAY=#1 -I /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/include -I /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/module /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/sky130_fd_sc_hd.v /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/primitives.v  /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/module/testbench.v
```
## 2. Run the Simulation
```
cd /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/output/post_synth_sim/
```
## 3. Simulation waveforms can be viewed using GTKWave:
```
./post_synth_sim.out
```
