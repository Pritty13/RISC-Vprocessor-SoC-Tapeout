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


## Iverilog 
* Steps to install iverilog *
  
sudo apt-get update 

sudo apt-get install iverilog


# gtkwave 
* Steps to install gtkwave *
  
$ sudo apt-get update 

$ sudo apt install gtkwave 

