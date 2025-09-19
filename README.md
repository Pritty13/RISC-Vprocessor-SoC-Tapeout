# RISC-Vprocessor-SoC-Tapeout
Task-1 Create GitHub repo. Document summary of previous video in the GitHub repo 
Refer the following repo https://github.com/sukanyasmeher/sfal-vsd?tab=readme-ov-file#day-0--
tools-installation 
Task-2 Install tools listed in this document using the machine configuration mentioned. Update 
your GitHub repo with Tool snapshot ----—-----------------------------------------Installation instructions ------------------------------------------------ 
Oracle virtual machine link 
https://www.virtualbox.org/wiki/Downloads 
System Check 
6GB RAM, 50 GB HDD 
Ubuntu 20.04+ 
4vCPU 
Tool check 
Yosys 
$ sudo apt-get update 
$ git clone https://github.com/YosysHQ/yosys.git 
$ cd yosys 
$ sudo apt install make (If make is not installed please install it)  
$ sudo apt-get install build-essential clang bison flex \ 
libreadline-dev gawk tcl-dev libffi-dev git \ 
graphviz xdot pkg-config python3 libboost-system-dev \ 
libboost-python-dev libboost-filesystem-dev zlib1g-dev 
$ make config-gcc 
$ make  
$ sudo make install 
Iverilog 
Steps to install iverilog 
sudo apt-get update 
sudo apt-get install iverilog 
gtkwave 
Steps to install gtkwave 
sudo apt-get update 
sudo apt install gtkwave 
