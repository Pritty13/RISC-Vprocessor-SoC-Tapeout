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


## gtkwave 
  
$ sudo apt-get update 

$ sudo apt install gtkwave 

## NGSpice
# ============================
# Step 0: Optional - Update system
# ============================
sudo apt update
sudo apt upgrade -y

# ============================
# Step 1: Remove old ngspice (if installed)
# ============================
sudo apt remove --purge ngspice -y
sudo apt autoremove -y
which ngspice   # should return nothing

# ============================
# Step 2: Install required build dependencies
# ============================
sudo apt install -y build-essential git autoconf automake libtool \
    xorg-dev libx11-dev libxext-dev libxft-dev libxpm-dev \
    libreadline-dev libfftw3-dev libpng-dev

# ============================
# Step 3: Prepare for VirtualBox X11 (GUI plotting)
# ============================
sudo apt install -y xorg openbox x11-apps
# Optional: Test X11 display
xclock   # Should pop up a small clock window

# ============================
# Step 4: Install VirtualBox Guest Additions (if running in VM)
# ============================
sudo apt install -y dkms linux-headers-$(uname -r)
sudo mkdir -p /media/cdrom
sudo mount /dev/cdrom /media/cdrom
sudo /media/cdrom/VBoxLinuxAdditions.run
sudo reboot

# ============================
# Step 5: Extract ngspice source
# ============================
cd ~/Downloads
tar -xzf ngspice-45.2.tar.gz
cd ngspice-45.2

# ============================
# Step 6: Configure build with X11 and XSPICE support
# ============================
./configure --prefix=/usr/local --with-x --enable-xspice --enable-cider

# ============================
# Step 7: Compile ngspice
# ============================
make

# ============================
# Step 8: Install ngspice
# ============================
sudo make install

# ============================
# Step 9: Verify installation
# ============================
ngspice -v    # Should display ngspice-45.2

# ============================
# Step 10: Test GUI plotting
# ============================
ngspice
# At the ngspice prompt, try:
```
help
quit
```



![gtkwave install](https://github.com/user-attachments/assets/13abd841-7aba-440d-bd6a-62997ea80f3c)
