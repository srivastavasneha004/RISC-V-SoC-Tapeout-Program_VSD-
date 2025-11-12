# RISC-V Reference SoC Tapeout Program VSD

## Tools Installation

All the instructions for installation of required tools can be found here:

### System Requirements

- **6 GB RAM**
- **50 GB HDD**
- **Ubuntu 20.04 or higher**
- **4 vCPU**

### Resizing the Ubuntu window to fit the screen

```bash
$ sudo apt update
$ sudo apt install build-essential dkms linux-headers-$(uname -r)
$ cd /media/spatha/VBox_GAs_7.1.8/
$ ./autorun.sh
```

---

## TOOL CHECK

### Yosys

```bash
$ sudo apt-get update
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys
$ sudo apt install make               # If make is not installed
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make config-gcc
# Yosys build depends on a Git submodule called abc, which hasn't been initialized yet. 
# You need to run the following command before running make
$ git submodule update --init --recursive
$ make 
$ sudo make install
```

![Yosys Installation](assets/yosys.jpg)

### Iverilog

```bash
$ sudo apt-get update
$ sudo apt-get install iverilog
```

![Iverilog Installation](assets/Iverilog.jpg)

### gtkwave

```bash
$ sudo apt-get update
$ sudo apt install gtkwave
```

![GTKWave Installation](assets/gtkwave.jpg)

---

## 🌟 Week 0 Summary

Successfully completed the setup and installation of all required EDA tools:

- ✅ **Yosys** - Open-source RTL synthesis tool
- ✅ **Iverilog** - Icarus Verilog HDL simulator
- ✅ **GTKWave** - Waveform viewer for simulation results

These tools form the foundation for the upcoming RTL to GDSII design flow in the RISC-V SoC Tapeout Program.