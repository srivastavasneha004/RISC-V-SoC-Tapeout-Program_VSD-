# RTL Design And Synthesis Workshop Using Sky130

![RTL Workshop](https://img.shields.io/badge/RTL-Workshop-blue) ![Verilog](https://img.shields.io/badge/Language-Verilog-green) ![Sky130](https://img.shields.io/badge/PDK-Sky130-orange) ![License](https://img.shields.io/badge/License-CC--BY--4.0-red)

Welcome to the **RTL Workshop**, a comprehensive hands-on learning series focused on Verilog RTL design, simulation, synthesis, and digital circuit optimization using the Sky130 PDK. This repository documents my successful completion of the RTL design workshop, showcasing practical implementations and synthesis results.

---

## Table of Contents

- [About This Workshop](#about-this-workshop)
- [Prerequisites](#prerequisites)
- [Workshop Structure](#workshop-structure)
- [Tools Used](#tools-used)
- [Key Learning Outcomes](#key-learning-outcomes)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [License](#license)
- [Acknowledgements](#acknowledgements)

---

## About This Workshop

This workshop is designed for students, engineers, and hobbyists who want to master:

- **Verilog RTL Design**: Writing efficient and synthesizable Verilog code
- **Simulation Techniques**: Using Icarus Verilog and GTKWave for comprehensive design verification
- **Logic Synthesis**: Leveraging Yosys synthesis tool with Sky130 open-source PDK
- **Digital Design Concepts**: Understanding testbenches, timing libraries, flip-flop coding styles, and optimization techniques
- **Industry Best Practices**: Following proper RTL coding guidelines and design methodologies

## Prerequisites

Before starting this workshop, ensure you have:

- ✅ Basic understanding of digital logic (gates, flip-flops, multiplexers, etc.)
- ✅ Familiarity with Linux/Windows command line interface
- ✅ Basic knowledge of hardware description languages (helpful but not mandatory)

### Required Tools:
- `git` - Version control
- `iverilog` - Verilog simulation
- `gtkwave` - Waveform viewer
- `yosys` - Logic synthesis
- Text editor (VS Code, vim, etc.)

---

## Workshop Structure

The workshop is organized into 5 comprehensive days, each building upon previous concepts:

| Day | Topic | Key Concepts |
|-----|-------|-------------|
| **[Day 1](Day_1/README.md)** | Introduction to Verilog RTL Design & Synthesis | Simulators, testbenches, basic synthesis |
| **[Day 2](Day_2/README.md)** | Timing Libraries & Flip-Flop Coding | Sky130 PDK, hierarchical vs flat synthesis, DFF styles |
| **[Day 3](Day_3/README.md)** | Combinational and Sequential Optimization | Constant propagation, state optimization, cloning |
| **[Day 4](Day_4/README.md)** | Gate-Level Simulation & Synthesis-Simulation Mismatch | GLS, blocking vs non-blocking, debugging |
| **[Day 5](Day_5/README.md)** | Advanced Synthesis Optimization | If-else optimization, loops, generate blocks |

Each day includes:
- 📖 **Detailed theory explanations** with real-world examples
- 🛠️ **Hands-on practical labs** with step-by-step instructions
- 📊 **Synthesis results and waveforms** demonstrating concepts
- 💡 **Best practices and common pitfalls** to avoid
- 🔍 **Code analysis and optimization techniques**

---

## Tools Used

### Open Source EDA Tools
- **Icarus Verilog (iverilog)**: Fast and reliable Verilog simulator
- **GTKWave**: Comprehensive waveform viewer and analyzer
- **Yosys**: Advanced logic synthesis framework
- **Sky130 PDK**: Open-source process design kit from SkyWater

### Development Environment
- **Operating System**: Linux/Windows/WSL
- **Version Control**: Git
- **Documentation**: Markdown with GitHub integration

---

## Key Learning Outcomes

Upon completing this workshop, you will be able to:

### 🎯 **Design Skills**
- Write clean, synthesizable Verilog RTL code
- Create comprehensive testbenches for design verification
- Implement various digital building blocks (MUX, DFF, adders, etc.)

### 🔧 **Synthesis & Optimization**
- Perform logic synthesis using industry-standard tools
- Optimize designs for area, power, and timing
- Understand the impact of coding styles on synthesis results

### ✅ **Verification & Debug**
- Conduct thorough simulation and waveform analysis
- Perform gate-level simulation (GLS) for timing verification
- Debug synthesis-simulation mismatches effectively

### 📚 **Industry Knowledge**
- Understand timing library characteristics
- Apply proper RTL coding guidelines
- Use open-source PDK for realistic synthesis targets

---

## Repository Structure

```
RTL_Workshop/
├── README.md                 # Main documentation (this file)
├── LICENSE                   # Project license
├── Day_1/
│   ├── README.md            # Day 1 detailed documentation
│   ├── good_mux_waveform.jpg # Simulation waveforms
│   └── Netlist.jpg          # Synthesis results
├── Day_2/
│   ├── README.md            # Day 2 detailed documentation
│   ├── dff_waveform.jpg     # Flip-flop simulations
│   ├── dff_netlist.jpg      # DFF synthesis results
│   ├── hierarchical.png     # Hierarchical synthesis
│   ├── flattened.png        # Flattened synthesis
│   └── sky130PDK.jpg        # PDK exploration
├── Day_3/
│   ├── README.md            # Day 3 detailed documentation
│   ├── opt.jpg              # Optimization lab 1
│   ├── opt2.jpg             # Optimization lab 2
│   ├── opt3.jpg             # Optimization lab 3
│   ├── opt4.jpg             # Optimization lab 4
│   ├── dff_const1.jpg       # Sequential opt 1
│   └── dff_const2.jpg       # Sequential opt 2
├── Day_4/
│   ├── README.md            # Day 4 detailed documentation
│   ├── lab1.jpg             # GLS lab 1
│   ├── lab2.jpg             # GLS lab 2
│   ├── lab3.jpg             # GLS lab 3
│   ├── lab4.jpg             # Blocking vs non-blocking
│   ├── lab5.jpg             # Synthesis mismatch
│   ├── lab6.jpg             # Advanced debugging
│   └── lab7.jpg             # Final synthesis
└── Day_5/
    ├── README.md            # Day 5 detailed documentation
    ├── in_comp_if.jpg       # Incomplete if statements
    ├── incomp_synth.jpg     # Synthesis results
    ├── icomp2.jpg           # Nested if-else
    ├── incomp2synth.jpg     # Advanced synthesis
    ├── compcase.jpg         # Complete case statements
    ├── compcase_synth.jpg   # Case synthesis
    ├── partial.jpg          # Partial assignments
    ├── partial_co.png       # Partial synthesis
    ├── badcase.jpg          # Bad case example
    ├── mux_generate.jpg     # Generate blocks
    ├── demux-case.jpg       # Demux implementations
    ├── demux-generate.jpg   # Generate demux
    └── rca_org.jpg          # Ripple carry adder
```

---

## Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/srivastavasneha004/RTL_Workshop.git
cd RTL_Workshop
```

### 2. Set Up Your Environment
```bash
# Install required tools (Ubuntu/Debian)
sudo apt update
sudo apt install iverilog gtkwave yosys git

# For other distributions, use appropriate package manager
```

### 3. Start with Day 1
```bash
cd Day_1
# Follow the README.md instructions for detailed labs
```

### 4. Explore Each Day Sequentially
Each day builds upon previous concepts, so it's recommended to follow them in order.

---

## License

This project is licensed under the **Creative Commons Attribution 4.0 International License** - see the [LICENSE](LICENSE) file for details.

You are free to:
- **Share** — copy and redistribute the material in any medium or format
- **Adapt** — remix, transform, and build upon the material

Under the following terms:
- **Attribution** — You must give appropriate credit and indicate if changes were made

---

## Acknowledgements

### 🙏 **Special Thanks**

- **[VSD-IAT](https://www.vlsisystemdesign.com/)** - For organizing this comprehensive workshop
- **[Kunal Ghosh](https://github.com/kunalg123)** - Workshop instructor and VLSI System Design founder
- **[Shon Taware](https://github.com/ShonTaware)** - Technical guidance and mentorship

### 🛠️ **Open Source Community**
- **Yosys Development Team** - For the excellent synthesis framework
- **Icarus Verilog Contributors** - For reliable simulation tools
- **SkyWater Technology** - For the open-source Sky130 PDK
- **GTKWave Team** - For the comprehensive waveform viewer

### 📚 **Resources & References**
- [Sky130 PDK Documentation](https://skywater-pdk.readthedocs.io/)
- [Yosys Manual](https://yosyshq.net/yosys/documentation.html)
- [Icarus Verilog Documentation](https://iverilog.icarus.com/)

---

## Author

**Sneha Srivastava**
- GitHub: [@srivastavasneha004](https://github.com/srivastavasneha004)
- Repository: [RTL_Workshop](https://github.com/srivastavasneha004/RTL_Workshop)

---

## 🚀 Ready to Start?

Begin your RTL design journey with [Day 1: Introduction to Verilog RTL Design & Synthesis](Day_1/README.md)!

---

<div align="center">

**⭐ If you find this repository helpful, please consider giving it a star! ⭐**

*Happy Learning! 🎯*

</div>