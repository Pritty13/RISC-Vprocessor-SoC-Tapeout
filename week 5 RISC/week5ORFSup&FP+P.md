# **Week 5 Task – OpenROAD Flow Setup and Floorplan + Placement**

---

## **Objective**
To set up the **OpenROAD Flow Scripts** environment and execute the **Floorplan** and **Placement** stages of the physical design flow.

This task transitions you from **SPICE-level transistor design (Week 4)** to **backend implementation**, where logic is converted into an actual physical layout.

---

## **Why This Task Is Important**
After understanding how timing arises from transistor-level circuits, it’s time to see how those circuits are **physically realized on silicon**.

This task introduces you to **OpenROAD**, an open-source RTL-to-GDSII flow widely used in academic and industrial research.

Learning to perform floorplanning and placement helps you understand:

- How design constraints are applied before routing.  
- How standard cells are arranged to minimize delay, area, and congestion.  
- How physical design choices affect timing and manufacturability.

This is your **first step toward a full physical implementation flow** in VLSI design.

---

## **Task Reference**
Use the following repository as your reference for installation and running the required flow steps:

🔗 **OpenROAD Reference:**  
[https://github.com/spatha0011/spatha_vsdhdp/blob/main/Day14/README.md](https://github.com/spatha0011/spatha_vsdhdp/blob/main/Day14/README.md)

---

## **Task Components**

### **1. Install OpenROAD Flow Scripts**
- Clone and install **OpenROAD Flow Scripts** on your Linux system.  
- Follow all prerequisite installations as listed in the reference repository.  
- Verify successful setup by launching the OpenROAD environment (`flow.tcl` or equivalent).

---

### **2. Execute Floorplan and Placement (Strictly Only These Two Stages)**
- Run the OpenROAD flow **up to the Floorplan and Placement stages only**.  
  ⚠️ *Do not proceed to routing or any later stages this week.*
- Confirm:
  - ✅ Core area and die dimensions are generated.  
  - ✅ Standard cells are placed successfully.  
- Review generated **logs** and **intermediate design files**.

---

## **Deliverables**

Submit documentation showing **clear installation and execution proof**:

### **1. Terminal Snapshots**
Include screenshots showing:

#### 1. Clone the OpenROAD Repository

```bash
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD-flow-scripts
cd OpenROAD-flow-scripts
```

#### 2. Run the Setup Script

```bash
sudo ./setup.sh
```
![set up script 1](https://github.com/user-attachments/assets/f585fd1c-44e2-4504-bacd-663f954ab3b5)


#### 3. Build OpenROAD

```bash
./build_openroad.sh --local
```

![build openroad 2](https://github.com/user-attachments/assets/64d6df50-5c6c-401e-a6d7-ae7b11e8c054)

#### 4. Verify Installation

```bash
source ./env.sh
yosys -help
```
![yosys 3](https://github.com/user-attachments/assets/26e1b262-27ef-4aa1-a530-c4f1ee76fbf3)

### **2. Images / Outputs**

### 1. Run the OpenROAD Flow

```bash
cd flow
make
```


### 2. Launch the graphical user interface (GUI) to visualize the final layout

```bash
 make gui_final
```

✅ Installation Complete! You can now explore the full RTL-to-GDSII flow using OpenROAD.

### `ORFS Directory Structure and File formats`

OpenROAD-flow-scripts/

```plaintext
├── OpenROAD-flow-scripts             
│   ├── docker           -> It has Docker based installation, run scripts and all saved here
│   ├── docs             -> Documentation for OpenROAD or its flow scripts.  
│   ├── flow             -> Files related to run RTL to GDS flow  
|   ├── jenkins          -> It contains the regression test designed for each build update
│   ├── tools            -> It contains all the required tools to run RTL to GDS flow
│   ├── etc              -> Has the dependency installer script and other things
│   ├── setup_env.sh     -> Its the source file to source all our OpenROAD rules to run the RTL to GDS flow
```
Inside the `flow/` Directory

```plaintext
├── flow           
│   ├── design           -> It has built-in examples from RTL to GDS flow across different technology nodes
│   ├── makefile         -> The automated flow runs through makefile setup
│   ├── platform         -> It has different technology note libraries, lef files, GDS etc 
|   ├── tutorials        
│   ├── util            
│   ├── scripts                 
```

### **3. Short Summary (3–4 lines)**
I installed the OpenROAD Flow Scripts on my Linux system and successfully set up the environment following the reference repository. 
I executed the flow up to the Floorplan and Placement stages, verifying the generation of core area, die dimensions, and proper standard cell placement.
Initial dependency issues were resolved by reinstalling missing packages, and the setup completed without errors.

---

## **Expected Outcome**
By the end of **Week 5**, you will have:

- ✅ Successfully installed **OpenROAD Flow Scripts**  
- ✅ Executed and verified **Floorplan + Placement** stages  
- ✅ Produced visual and logged evidence of your working environment  

---

**End of Week 5 Task**
