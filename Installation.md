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

```bash
sudo apt update
sudo apt install build-essential dkms linux-headers-$(uname -r)
cd /media/$USER/VBox_GAs_*/   # Adjust version if needed
./autorun.sh


# Update packages
sudo apt-get update

# Clone repository
git clone https://github.com/YosysHQ/yosys.git
cd yosys

# Install dependencies
sudo apt-get install build-essential make clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 \
    libboost-system-dev libboost-python-dev \
    libboost-filesystem-dev zlib1g-dev

# Configure build
make config-gcc

# Initialize submodules
git submodule update --init --recursive

# Build and install
make
sudo make install

sudo apt-get update
sudo apt-get install iverilog


sudo apt-get update
sudo apt install gtkwave

