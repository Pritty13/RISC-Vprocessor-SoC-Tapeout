
# Introduction to the VSDBabySoC

VSDBabySoC is a small yet powerful RISCV-based SoC. The main purpose of designing such a small SoC is to test three open-source IP cores together for the first time and calibrate the analog part of it. VSDBabySoC contains one RVMYTH microprocessor, an 8x-PLL to generate a stable clock, and a 10-bit DAC to communicate with other analog devices.

<img width="1536" height="1024" alt="BabySoC Architecture Block Diagram" src="https://github.com/user-attachments/assets/b025b168-a482-4684-8fe9-b848289b2614" />

## Problem statement

This work discusses the different aspects of designing a small SoC based on RVMYTH (a RISCV-based processor). This SoC will leverage a PLL as its clock generator and controller and a 10-bit DAC as a way to talk to the outside world. Other electrical devices with proper analog input like televisions, and mobile phones could manipulate DAC output and provide users with music sound or video frames. At the end of the day, it is possible to use this small fully open-source and well-documented SoC which has been fabricated under Sky130 technology, for educational purposes.

## What is SoC

An SoC is a single-die chip that has some different IP cores on it. These IPs could vary from microprocessors (completely digital) to 5G broadband modems (completely analog).

## What is RVMYTH

RVMYTH core is a simple RISCV-based CPU, introduced in a workshop by RedwoodEDA and VSD. During a 5-day workshop students (including middle-schoolers) managed to create a processor from scratch. The workshop used the TLV for faster development. All of the present and future contributions to the IP will be done by students and under open-source licenses.

## What is PLL

A phase-locked loop or PLL is a control system that generates an output signal whose phase is related to the phase of an input signal. PLLs are widely used for synchronization purposes, including clock generation and distribution.

## What is DAC

A digital-to-analog converter or DAC is a system that converts a digital signal into an analog signal. DACs are widely used in modern communication systems enabling the generation of digitally-defined transmission signals. As a result, high-speed DACs are used for mobile communications and ultra-high-speed DACs are employed in optical communications systems.

# CODES FOR SIMULATION 

## RYMYTH Simulation code : 
```
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC$ cd /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ iverilog mythcore_test.v tb_mythcore_test.v
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ .a/.out
bash: .a/.out: No such file or directory
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ ./a.out
VCD info: dumpfile tb_mythcore_test.vcd opened for output.
tb_mythcore_test.v:22: $finish called at 2012000 (1ps)
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ gtkwave tb_mythcore_test.vcd

GTKWave Analyzer v3.3.116 (w)1999-2023 BSI
```
## AVSDAC Simulation code : 
```
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ iverilog avsddac.v avsddac_tb_test.v
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ ./a.out
VCD info: dumpfile avsddac_tb_test.vcd opened for output.
avsddac_tb_test.v:41: $finish called at 300000 (1ps)
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ gtkwave avsddac_tb_test.vcd

GTKWave Analyzer v3.3.116 (w)1999-2023 BSI
```
## RVMYTH and DAC integration Simulation code : 
```
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsdpll_interface/verilog$ cd /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ iverilog rvmyth_avsddac.v rvmyth_avsddac_tb.v
rvmyth_avsddac_tb.v: No such file or directory
Preprocessor failed with 1 errors.
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ ls
a.out        avsddac_tb_test.v    avsddac.v   mythcore_test_gen.v  pseudo_rand_gen.sv  rvmyth_avsddac_TB.v  rvmyth_avsddac.vcd  sandpiper.vh   sp_verilog.vh       tb_mythcore_test.vcd
avsddac.lib  avsddac_tb_test.vcd  clk_gate.v  mythcore_test.v      pseudo_rand.sv      rvmyth_avsddac.v     sandpiper_gen.vh    sp_default.vh  tb_mythcore_test.v  verilog_to_lib.pl

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ iverilog rvmyth_avsddac.v rvmyth_avsddac_TB.v

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ ./a.out

VCD info: dumpfile avsddac_tb_test.vcd opened for output.
avsddac_tb_test.v:41: $finish called at 300000 (1ps)

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ gtkwave avsddac_tb_test.vcd

GTKWave Analyzer v3.3.116 (w)1999-2023 BSI
```

## PLL Simulation code : 
```
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsddac_interface/iverilog/Pre-synthesis$ cd /home/pritty/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsdpll_interface/verilog

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsdpll_interface/verilog$ iverilog avsd_pll_1v8.v pll_tb.v

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsdpll_interface/verilog$ ./a.out

VCD info: dumpfile test.vcd opened for output.
pll_tb.v:59: $finish called at 56666000 (1ps)

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsdpll_interface/verilog$ gtkwave test.vcd

GTKWave Analyzer v3.3.116 (w)1999-2023 BSI

```
## RVMYTH and PLL integration Simulation code : 
```
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsdpll_interface/verilog$ iverilog rvmyth_pll.v rvmyth_pll_tb.v

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsdpll_interface/verilog$ ./a.out

VCD info: dumpfile test1.vcd opened for output.
rvmyth_pll_tb.v:60: $finish called at 56666000 (1ps)

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/rvmyth_avsdpll_interface/verilog$ gtkwave test1.vcd

GTKWave Analyzer v3.3.116 (w)1999-2023 BSI
```
## BabySoC Simulation Code:
```
pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC/src/module$ cd ~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC$ ls
images  LICENSE  Makefile  output  README.md  src

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC$ make pre_synth_sim
if [ ! -f "output/pre_synth_sim/pre_synth_sim.vcd" ]; then \
	mkdir -p output/pre_synth_sim; \
	iverilog -o output/pre_synth_sim/pre_synth_sim.out -DPRE_SYNTH_SIM \
		src/module/testbench.v \
		-I src/include -I src/module -I output/compiled_tlv; \
	cd output/pre_synth_sim; ./pre_synth_sim.out; \
fi

pritty@PrittyRISC-V:~/vsdpritty/sky130RTLDesignAndSynthesisWorkshop/RISCV_SOC/VSDBabySoC$  gtkwave output/pre_synth_sim/pre_synth_sim.vcd

GTKWave Analyzer v3.3.116 (w)1999-2023 BSI
```

# OUTPUT Waveforms BabySoc:

## RVMYTH
![rvmyth_proc output with code](https://github.com/user-attachments/assets/864ca7cf-defd-4ad7-aa56-3c5eaba61b27)


## DAC
![DAC output simulation with code](https://github.com/user-attachments/assets/28cac4f6-2083-4cde-bda1-af6d0dc20c55)

## RVMYTH and DAC

![rvmyth_avsddac output simulation with code](https://github.com/user-attachments/assets/60c629ce-c6cb-4050-9176-34f82722bac7)

## PLL

![pll output simulation with code](https://github.com/user-attachments/assets/ce87ef18-5a61-4447-aa3d-658e63815a4a)

## RVMYTH and PLL
![rvmyth_pll output simulation  with code](https://github.com/user-attachments/assets/af56f53c-8a3c-45d4-9419-36228040890d)


## Baby SoC

![babySoC Output with code](https://github.com/user-attachments/assets/0c477077-ac08-4ef7-a92a-6301b358a58b)


# Short Explanation for Baby SoC:

The BabySoC successfully demonstrates the integration of its three core components—RVMYTH processor, PLL, and 10-bit DAC. Simulation and synthesis results confirm correct processor operation, stable clock generation, and accurate digital-to-analog conversion. The functional model and RTL outputs validate data flow, timing synchronization, and signal conversion, showcasing a working miniature SoC that effectively bridges digital processing and analog interfacing—proving BabySoC as a reliable educational SoC prototype.


