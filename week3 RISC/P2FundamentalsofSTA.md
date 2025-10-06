# 🧠 Week 3 Task – Post-Synthesis GLS & STA Fundamentals  
### Part 2: Fundamentals of STA (Static Timing Analysis)

---

## 📘 Overview

**Static Timing Analysis (STA)** is a method used to verify the **timing performance** of a digital circuit **without simulation**.  
It checks **all possible timing paths** in a design to ensure the circuit meets **setup** and **hold** timing requirements.

---

## 🕒 Key Timing Concepts

- **Clock Period (T):** Time between two consecutive clock edges.  
- **Propagation Delay (tpd):** Time for a signal to propagate through combinational logic.  
- **Setup Time (tsu):** Minimum time data must be stable **before** the clock edge.  
- **Hold Time (th):** Minimum time data must remain stable **after** the clock edge.  
- **Clock Skew:** Difference in arrival times of the clock at different registers.

---

## ⚙️ Setup and Hold Checks

### ✅ **Setup Check**
Ensures data arrives **before** the capturing clock edge.

\[
T_{clk} \geq T_{clk\_q} + T_{comb} + T_{setup}
\]

- **Violation:** Data is **late** → incorrect value may be captured.

### ✅ **Hold Check**
Ensures data remains stable **after** the clock edge.

\[
T_{clk\_q} + T_{comb} \geq T_{hold}
\]

- **Violation:** Data changes **too early** → capturing invalid data.

---

## ⏱️ Slack

**Slack = Required Time – Arrival Time**

- 🟢 **Positive Slack:** Timing met (safe)  
- ⚪ **Zero Slack:** On the timing boundary  
- 🔴 **Negative Slack:** Timing violation (failure)

Two main types:
- **Setup Slack**
- **Hold Slack**

---

## 🕹️ Clock Definitions

Clock definitions guide STA tools on timing relationships.

- Clock **period**
- Clock **waveform** (rise/fall edges)
- Clock **latency**
- **Generated clocks** (from PLLs, dividers)

Used by STA to determine **launch** and **capture** times for data paths.

---

## 🔗 Path-Based Analysis

STA examines all **register-to-register** or **I/O** paths for timing violations.

### Main Path Types:
1. **Register-to-Register (Sequential)**  
2. **Input-to-Register**  
3. **Register-to-Output**  
4. **Input-to-Output (Combinational)**  

Each path is checked separately for **setup** and **hold** timing.

---

## 💡 Why STA Matters

- Fast and **exhaustive** (no need for test vectors).  
- Detects **critical paths** and **timing bottlenecks**.  
- Helps fix violations by:
  - Buffer insertion
  - Cell resizing
  - Adjusting clock constraints  
- A **mandatory step** before chip **sign-off or tape-out**.

---

## 📗 Reference
- **Course:** [STA Fundamentals – VLSI Academy (Udemy)](https://www.udemy.com/course/vlsi-academy-sta-checks/?couponCode=F960AEDD365E0CD12546)
- **Focus Areas:**
  - Setup & Hold checks  
  - Slack  
  - Clock Definitions  
  - Path-Based Analysis

---

**🧩 Summary:**  
STA ensures every timing path in a chip meets setup and hold constraints, preventing functional errors in fabricated silicon. It’s an essential verification step bridging **logic design** and **physical implementation**.
