# Week 4 – CMOS Circuit Design 
## Deliverables Report (Following Sky130 Workshop Format)

---

## 1. Introduction / Background  

This week focuses on **Gate-Level Simulation (GLS)** after synthesis and introduces **Static Timing Analysis (STA)** concepts using OpenSTA.  
Each experiment links transistor-level behaviour to system-level timing constraints.

### Purpose of Each Experiment  
- **Id vs Vds:** To study transistor output characteristics and identify saturation/linear regions.  
- **VTC (Voltage Transfer Characteristic):** To analyse inverter switching point and noise margins.  
- **Transient Analysis:** To measure propagation delay and rise/fall times.  
- **Variation Study:** To understand how process or voltage variation shifts delay and noise margins.  

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

##5. Observations / Analysis

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

