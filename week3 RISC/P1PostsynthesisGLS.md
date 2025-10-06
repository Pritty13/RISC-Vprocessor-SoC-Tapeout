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
![post synthesis yosys GLS 1](https://github.com/user-attachments/assets/7e8b1891-6f06-4681-829c-c60d23093b9d)


### 2. Read top-level RTL and modules
```
read_verilog /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/module/vsdbabysoc.v
```
![post synthesis yosys GLS 2](https://github.com/user-attachments/assets/b22d4ed2-73e9-4130-8814-39b1447d73b6)

```
read_verilog -I /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/module/rvmyth.v
```
![post synthesis yosys GLS 2 1](https://github.com/user-attachments/assets/401937ba-3764-450f-9b1f-051d17c689aa)

```
read_verilog -I /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/module/clk_gate.v
```
![post synthesis yosys GLS 2 2](https://github.com/user-attachments/assets/aa99d5dc-1618-4421-84e9-7a75bbc501ab)

### 3. Read standard cell and IP libraries
```
read_liberty -lib /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/avsdpll.lib
```
![post synthesis yosys GLS 3](https://github.com/user-attachments/assets/23ed418c-bbbf-401e-b81e-856782c3aaf5)

```
read_liberty -lib /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/avsddac.lib
```
![post synthesis yosys GLS 3 1](https://github.com/user-attachments/assets/2cb9d331-7bc8-49a5-9df4-14cb7523e0ad)

```
read_liberty -lib /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![post synthesis yosys GLS 3 2](https://github.com/user-attachments/assets/175868e5-d63f-4e17-a22c-1e07839b66c3)

### 4. Synthesize the top-level design
```
synth -top vsdbabysoc
```
![post synthesis yosys GLS 4](https://github.com/user-attachments/assets/daa4043a-b9a9-479a-a620-22247a28664d)
![post synthesis yosys GLS 4 1](https://github.com/user-attachments/assets/07a94683-2f10-4286-bea1-2cebb18ddb9a)
![post synthesis yosys GLS 4 2](https://github.com/user-attachments/assets/ea03e21b-c1f7-460c-a863-32cdb7b721d1)
![post synthesis yosys GLS 4 3 clk_gate](https://github.com/user-attachments/assets/3120385c-aea4-44dc-9380-5461604291a6)
![post synthesis yosys GLS 4 4 rvmyth](https://github.com/user-attachments/assets/b16bea88-5d53-4bdc-8d13-3e577a9feaea)
![post synthesis yosys GLS 4 5 babysoc](https://github.com/user-attachments/assets/5366818a-718f-4430-8e69-e17cfc47cba0)
![post synthesis yosys GLS 4 6 designhierarachy](https://github.com/user-attachments/assets/6433884f-18c2-4294-bf91-c2250ba28414)
![post synthesis yosys GLS 4 7](https://github.com/user-attachments/assets/ab6502ce-b2e4-4b02-8a58-5802fbfd6952)

### 5. Map D flip-flops to library
```
dfflibmap -liberty /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![post synthesis yosys GLS 5](https://github.com/user-attachments/assets/84245be7-4d1b-48ee-876e-cc38d66cb88b)

![post synthesis yosys GLS 5 1](https://github.com/user-attachments/assets/a9724175-b24c-4db0-adaf-45ab18060480)

### 6. Technology mapping and optimization
```
abc -liberty /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib \
    -script +strash;scorr;ifraig;retime;{D};strash;dch,-f;map,-M,1,{D}
```
![post synthesis yosys GLS 6](https://github.com/user-attachments/assets/3f489fab-b665-43f2-8076-dd7cf38e315d)
![post synthesis yosys GLS 6 1](https://github.com/user-attachments/assets/57dbfcee-a316-42e1-8ec0-311c06a059a0)

### 7. Flatten hierarchy and clean design
```
flatten
setundef -zero
clean -purge
rename -enumerate
```
![post synthesis yosys GLS 7](https://github.com/user-attachments/assets/aa6370f5-22ba-4301-8665-1e7c3c5e39f4)

### 8. Get design statistics
```
stat
```
![post synthesis yosys GLS 8](https://github.com/user-attachments/assets/5ca39573-ab34-4d52-a3ee-03228ec9e110)

![post synthesis yosys GLS 8 1](https://github.com/user-attachments/assets/091518b9-114f-4255-96d0-fb7d9eaaf55f)

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
![post synthesis yosys GLS 9](https://github.com/user-attachments/assets/397d44e0-cb45-40ce-878b-5bae48141df3)
![post synthesis yosys GLS 9 1](https://github.com/user-attachments/assets/994e8c7e-6143-4321-8c0f-dd2e921b143a)
![post synthesis yosys GLS 9 2](https://github.com/user-attachments/assets/ac93e348-bcff-4b09-85c6-0a1803f6d150)
