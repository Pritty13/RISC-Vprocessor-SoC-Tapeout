# RISC-Vprocessor-SoC-Tapeout

This repository documents the setup and tool installation required for the **RISC-V Reference SoC Tapeout Program** conducted by VLSI System Design (VSD).  

---

## System Requirements
- **OS**: Ubuntu 20.04 or higher  
- **RAM**: 6 GB  
- **HDD**: 50 GB free space  
- **CPU**: 4 vCPUs  

---

## Resizing the Ubuntu Window to Fit Screen
Run the following to install VirtualBox Guest Additions (inside Ubuntu VM):

# Tool check 

## Yosys 
$ sudo apt-get update 

$ git clone https://github.com/YosysHQ/yosys.git 

$ cd yosys 

$ sudo apt install make   

$ sudo apt-get install build-essential clang bison flex \ 
libreadline-dev gawk tcl-dev libffi-dev git \ 
graphviz xdot pkg-config python3 libboost-system-dev \ 
libboost-python-dev libboost-filesystem-dev zlib1g-dev 

$ make config-gcc 

$ make  

$ sudo make install 

![yosys install](https://github.com/user-attachments/assets/4e7d2d5d-8f01-41a1-b5ee-0480314ea71b)


## Iverilog 
  
sudo apt-get update 

sudo apt-get install iverilog

![iverilog install](https://github.com/user-attachments/assets/d66d3bdf-2b25-49e0-a1b3-7bd20de6c713)


# gtkwave 
  
$ sudo apt-get update 

$ sudo apt install gtkwave 


![gtkwave install](https://github.com/user-attachments/assets/13abd841-7aba-440d-bd6a-62997ea80f3c)

# ngspice


![ngspice install](https://github.com/user-attachments/assets/eed7267c-7a8a-426a-b51c-b3e80400cd69)


