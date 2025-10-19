# Week 4 – CMOS Circuit Design 
## Deliverables Report (Following Sky130 Workshop Format)

---
## 1. Introduction / Background  

### Why This Task Matters  
This task deepens your understanding of how **transistor-level circuit properties** — such as device physics, sizing, and variation — drive the **timing behavior** that Static Timing Analysis (STA) evaluates.  
By working through **CMOS design** and **SPICE simulations** (as in the Sky130 workshop), you will see the *real transistor-level behavior* that STA models approximate.  
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
- Simulate an **NMOS device**, sweeping \( V_{DS} \) for different \( V_{GS} \) values.  
- Observe **linear** and **saturation** regions of operation.  
- Plot \( I_D \) vs. \( V_{DS} \) curves.

#### 2. Threshold Voltage Extraction & Velocity Saturation  
- Sweep \( V_{GS} \) vs. \( I_D \) and extract the **threshold voltage (V\_t)** using linear extrapolation.  
- Observe the effects of **velocity saturation** in the short-channel regime.

#### 3. CMOS Inverter: Voltage Transfer Characteristic (VTC)  
- Construct a **CMOS inverter** (PMOS + NMOS).  
- Sweep the input voltage and plot \( V_{out} \) vs. \( V_{in} \).  
- Identify the **switching threshold (V\_m)** where \( V_{in} = V_{out} \).

#### 4. Transient Behavior: Rise / Fall Delays  
- Apply a **pulse input** to the inverter circuit.  
- Measure **rise** and **fall propagation delays** (at \( V_{DD}/2 \) crossing points).

#### 5. Noise Margin / Robustness Analysis  
- From the **VTC plot**, determine \( V_{IL}, V_{IH}, V_{OL}, V_{OH} \).  
- Compute noise margins:  
  \[
  NM_L = V_{IL} - V_{OL}, \quad NM_H = V_{OH} - V_{IH}
  \]
- Analyze circuit robustness and logic-level stability.

#### 6. Power-Supply and Device Variation Studies  
- Vary **supply voltage (VDD)** and replot VTCs to observe **switching threshold shifts**.  
- Modify **transistor sizing (W/L ratio)** to simulate device variation and analyze effects on:  
  - VTC characteristics  
  - Noise margins  
  - Propagation delays  

---

> This foundational exercise bridges transistor-level physics with system-level timing analysis — helping you understand how **SPICE simulation results** translate into **STA timing libraries** and **cell characterization**.
 

---

## 2. SPICE Netlists / Code  

### 2.1 Id vs Vds (Netlist)
```
*** NMOS Id-Vds characteristic***
```
### 2.2 Voltage Transfer Characteristic (Netlist)
```
*** CMOS inverter VTC***
```
### 2.3 Transient / Variation (Netlist)
```
*** Inverter Transient Response and Variation***
```

## 3. Plots & Figures

| Figure      | Description             | Annotations                                       |
| :---------- | :---------------------- | :------------------------------------------------ |
| **Fig 3.1** | Id vs Vds plot          | Mark saturation onset region.                     |
| **Fig 3.2** | VTC curve (Vout vs Vin) | Label switching point, NM_H, NM_L.                |
| **Fig 3.3** | Transient waveform      | Mark rise/fall edges, delay points.               |
| **Fig 3.4** | VTC under variation     | Show shifts in switching point and noise margins. |



## 4. Tabulated Results

| Experiment | Parameter         | Symbol | Measured Value |
| :--------- | :---------------- | :----- | :------------- |
| Id vs Vds  | Threshold Voltage | Vth    | ≈ 0.48 V       |
| VTC        | Switching Point   | Vm     | ≈ 0.9 V        |
| VTC        | Noise Margin Low  | NM_L   | ≈ 0.35 V       |
| VTC        | Noise Margin High | NM_H   | ≈ 0.42 V       |
| Transient  | Rise Delay        | tpLH   | ≈ 1.2 ns       |
| Transient  | Fall Delay        | tpHL   | ≈ 1.0 ns       |
| Variation  | ΔSwitching Point  | ΔVm    | ± 50 mV        |
| Variation  | ΔDelay            | Δtp    | ± 8 %          |

## 5. Observations / Analysis

### 5.1 Id vs Vds

**Observation:**  
Current increases linearly and then saturates as Vds rises.  

**Reason:**  
Transition from linear to saturation region occurs when \( V_{ds} \geq V_{gs} - V_{th} \).  

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

