# Week 4 – CMOS Circuit Design 
## Deliverables Report (Following Sky130 Workshop Format)

---
## 1. Introduction / Background  

### Why This Task Matters  
This task deepens your understanding of working through **CMOS design** and **SPICE simulations** (as in the Sky130 workshop), you will see the *real transistor-level behavior* that STA models approximate.  
This strengthens your intuition about **slack**, **delay**, **noise margins**, and **variation impacts** in digital design.

---

### Workshop Reference  
Download workshop collaterals from the link below:  
🔗 [Sky130 Circuit Design Workshop – GitHub Repository](https://github.com/kunalg123/sky130CircuitDesignWorkshop/)  

The workshop will be available on the **VSDIAT platform**, providing a hands-on environment for simulation and analysis.

---

### Task Components  
*(Adapted from the Sky130 Circuit Design Workshop)*  

You will carry out a sequence of CMOS design and SPICE simulation activities, mirroring the workflow in the Sky130 repository.

#### 1. MOSFET Behavior & Id vs. Vds Characteristics  
- Simulate an NMOS device, sweeping Vds for different Vgs values.   
- Observe **linear** and **saturation** regions of operation.  
- Plot Id vs. Vds curves.

#### 2. Threshold Voltage Extraction & Velocity Saturation  
- Sweep Vgs vs. Id and extract the threshold voltage (Vt) using linear extrapolation.  
- Observe the effects of velocity saturation in the short-channel regime.

#### 3. CMOS Inverter: Voltage Transfer Characteristic (VTC)  
- Construct a CMOS inverter (PMOS + NMOS).  
- Sweep the input voltage and plot Vout vs. Vin.  
- Identify the switching threshold (Vm) where Vin = Vout.

#### 4. Transient Behavior: Rise / Fall Delays  
- Apply a **pulse input** to the inverter circuit.  
- Measure **rise** and **fall propagation delays** (at \( V_{DD}/2 \) crossing points).

#### 5. Noise Margin / Robustness Analysis  
- From the **VTC plot**, determine
  - VIL (Input Low Voltage)  
  - VIH (Input High Voltage)  
  - VOL (Output Low Voltage)  
  - VOH (Output High Voltage) 
- Compute noise margins:  
  - NML = VIL - VOL  
  - NMH = VOH - VIH  
- Analyze circuit robustness and logic-level stability.

#### 6. Power-Supply and Device Variation Studies  
- Vary **supply voltage (VDD)** and replot VTCs to observe **switching threshold shifts**.  
- Modify **transistor sizing (W/L ratio)** to simulate device variation and analyze effects on:  
  - VTC characteristics  
  - Noise margins  
  - Propagation delays  

---

## 2. SPICE Netlists / Code  

### 2.1 Id vs Vds (Netlist)
```
*** NMOS Id-Vds characteristic***
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=5 l=2

R1 n1 in 55

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op
.dc Vdd 0 1.8 0.1 Vin 0 1.8 0.2

.control

run
display
setplot dc1
.endc

.end
```
### 2.2 Voltage Transfer Characteristic (Netlist)
```
*** CMOS inverter VTC***
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15

Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op

.dc Vin 0 1.8 0.01

.control
run
setplot dc1
display
.endc

.end
```
### 2.3 Transient / Variation (Netlist)
```
*** Inverter Transient Response and Variation***
*Model Description
.param temp=27

*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*Netlist Description

XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15

cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 PULSE(0V 1.8V 0 0.1ns 0.1ns 2ns 4ns)

*simulation commands

.tran 1n 10n

.control
run
.endc

.end
```

## 3. Plots & Figures

| Figure      | Description             | Annotations                                       |
| :---------- | :---------------------- | :------------------------------------------------ |
| **Fig 3.1** | Id vs Vds plot          | Mark saturation onset region.                     |
| **Fig 3.2** | Id vs Vgs plot (Long channel and short channel) | Thresold voltage          |
| **Fig 3.3** | VTC curve (Vout vs Vin) | Label switching point, NM_H, NM_L.                |
| **Fig 3.4** | Transient waveform      | Mark rise/fall edges, delay points.               |
| **Fig 3.5** | VTC under variation     | Show shifts in switching point and noise margins. |

![Id- Vds nfet w 0 39 l 0 15](https://github.com/user-attachments/assets/510b29a6-2505-4dde-a799-3bf96a201d78)
![Id- Vds nfet w 0 65 l  0 25](https://github.com/user-attachments/assets/f348d05b-9578-49bd-b921-739e90688c7a)

**Fig 3.1 Id vs Vds**

![Id- Vgs nfet w 0 39 l 0 15 LIN+Quad short channel](https://github.com/user-attachments/assets/9d1fd9eb-051e-4d7c-931b-54ca6dd00c9a)
![Id- Vgs nfet w 1 95 l 1 2 quad long channel](https://github.com/user-attachments/assets/33417716-fb22-4bfc-bf48-f6e901b913a3)

**Fig 3.2 Id vs Vgs (Long channel and short channel)**

![InvCMOSvtc Wp084 Wn036](https://github.com/user-attachments/assets/7f3ecd88-9905-4a6b-a275-7e883965ee8a)

 ![InvCMOS NM Wp1 Wn036](https://github.com/user-attachments/assets/5b6982f2-74e8-4b11-bb24-6525cf8de6f1)

 **Fig 3.3  VTC curve (Vout vs Vin) (Long channel and short channel)**

 ![InvCMOS trans Wp084 Wn036](https://github.com/user-attachments/assets/3e8eab5d-e953-4bed-97e3-4a2e64f25d80)

 **Fig 3.4 Transient waveform**

![InvCMOS Supply variations Wp1 Wn036](https://github.com/user-attachments/assets/f32809f4-adef-4db6-ad02-00751d350971)

 **Fig 3.5 VTC under variation**
 
## 4. Tabulated Results

| Experiment | Parameter         | Symbol | Measured Value |
| :--------- | :---------------- | :----- | :------------- |
| Id vs Vds  | Threshold Voltage | Vth    | ≈ 0.74 V       |
| VTC        | Switching Point   | Vm     | ≈ 0.0.87 V     |
| VTC        | Noise Margin Low  | NM_L   | ≈ 0.659 V       |
| VTC        | Noise Margin High | NM_H   | ≈ 0.33 V       |
| Transient  | Rise Delay        | tpLH   | ≈ 1.78 ns (Wp/Lp = 2.3 Wn/Ln)       |
| Transient  | Fall Delay        | tpHL   | ≈ 878 ns   (Wp/Lp = 2.3 Wn/Ln)      |
| Variation  | ΔSwitching Point  | ΔVm    | ± 50 mV        |
| Variation  | ΔDelay            | Δtp    | ± 8 %          |

## 5. Observations / Analysis

### 5.1 Id vs Vds

**Observation:**  
Current increases linearly and then saturates as Vds rises.  

**Reason:**  
Transition from linear to saturation region occurs when Vds ≥ (Vgs - Vth).  

**STA Tie-in:**  
Transistor current strength directly influences **cell delay models** in STA.

---

### 5.2 VTC Curve

**Observation:**  
Sharp transition observed around mid-rail (≈ 0.9 V).  

**Reason:**  
PMOS and NMOS currents balance at the **switching threshold**.  

**STA Tie-in:**  
Defines logic-level thresholds, affecting **noise margins** and **setup/hold timing**.

---

### 5.3 Transient Response

**Observation:**  
Measured rise/fall propagation delays during inverter switching.  

**Reason:**  
Load capacitance and transistor on-resistance limit the **transition speed**.  

**STA Tie-in:**  
Propagation delays correspond to **timing arcs** used in setup and hold checks.

---

### 5.4 Variation Study

**Observation:**  
Switching points and delays shift under ±10 % Vdd variation.  

**Reason:**  
Supply or process variation modifies **transistor drive current**.  

**STA Tie-in:**  
Variations create **timing uncertainty**, reducing slack and impacting **critical paths**.

---

## 6. Conclusions

- Transistor-level behaviour **directly constrains timing** in digital circuits.  
- **Setup and Hold margins** originate from measured propagation delays.  
- **Variations** in supply, temperature, and process shift delay and thresholds, impacting STA and timing closure.  
- Understanding **Id–Vds**, **VTC**, and **transient** characteristics is essential for building accurate **timing libraries**.

---

## 7. References / Citations

1. **SkyWater Sky130 PDK Documentation** – Device Models (`sky130_fd_pr`).  
2. **VSD Physical Design Workshop Notes** – Timing and STA Fundamentals.  
3. **OpenSTA User Guide** – Static Timing Analysis Commands.  
4. **Digital Integrated Circuits (2nd Edition)** – Jan M. Rabaey.  
5. **Sky130 Workshop GitHub Repository** – Documentation and structure reference.

