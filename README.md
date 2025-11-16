# 🖥️ RISC-V Reference SoC Tapeout Program VSD

Welcome to my journey through the **SoC Tapeout Program VSD**!  

This repository documents my week-by-week progress with tasks inside each week.  

"In this program, we learn to design a System-on-Chip (SoC) from basic RTL to GDSII using open-source tools. Part of India’s largest collaborative RISC-V tapeout initiative, empowering 3500+ participants to build silicon and advance the nation’s semiconductor ecosystem"

---

## 📅 Week 0 — Setup & Tools

| Task | Description | Status |
|------|-------------|--------|
| [**Task 0**](Week0/README.md) | 🛠️ [Tools Installation](Week0/README.md) — Installed **Iverilog**, **Yosys**, and **gtkWave** | ✅ Done |


### 🌟 Key Learnings from Week 0
- Installed and verified **open-source EDA tools** successfully.  
- Learned about **basic environment setup** for RTL design and synthesis.  
- Prepared the system for upcoming **RTL → GDSII flow experiments**.  

---

## 📅 Week 1 — RTL Synthesis & Gate-Level Simulation (GLS)

| Task | Description | Status |
|------|-------------|--------|
| [**Task 1**](Week1/README.md#-task-1--rtl-synthesis-mux-example) | 🔧 MUX synthesis in Yosys, Sky130 mapping, GLS netlist generation | ✅ Done |
| [**Task 2**](Week1/README.md#-task-2--constant-dff-mapping--gls) | 🎯 Constant DFF mapping (`const4.v`, `const5.v`) + GLS validation | ✅ Done |
| [**Task 3**](Week1/README.md#-task-3--mux-using-for-generate) | 💻 MUX using `for-generate`, RTL vs GLS verification | ✅ Done |

### 🌟 Key Learnings from Week 1

- Learned **Yosys synthesis flow**, RTL vs GLS verification, and scalable Verilog constructs.  
- Synthesized arithmetic circuits and optimized designs using ABC and Icarus Verilog with GTKWave.  
- Fixed synthesis-to-simulation mismatches and practiced mapping to SkyWater `sky130_fd_sc_hd` library.

---

## 📅 Week 2 — Fundamentals of SoC Design

| Task | Description | Status |
|------|-------------|--------|
| [**Task 1**](Week2/README.md#-fundamentals-of-system-on-chip-soc-design) | 📘 Write-up on SoC fundamentals | ✅ Done |
| [**Task 2**](Week2/README.md#-vsdbabysoc--a-tiny-but-powerful-risc-v-soc) | 📝 VSDBabySoC — RISC-V based SoC simulation and analysis | ✅ Done |

### 🌟 Key Learnings from Week 2

- Gained conceptual understanding of **SoC fundamentals** (CPU, memory, interconnect, peripherals).  
- Learned how **BabySoC** simplifies SoC design concepts and verified its behavior using simulation + GTKWave.  

---

## 📅 Week 3 — Advanced SoC Synthesis & Timing Analysis

| Task | Description | Status |
|------|-------------|--------|
| [**Task 1**](Week3#-gate-level-simulation-gls-of-babysoc- ) | ⚡ Pre- and Post-Synthesis Simulation for BabySoC | ✅ Done |
| [**Task 2**](Week3#-timing-graphs-using-opensta) | 📝 Short note on STA & OpenROAD | ✅ Done |

### 🌟 Key Learnings from Week 3

- Verified functional consistency between RTL and gate-level netlists using pre- and post-synthesis simulations.  
- Performed corner STA across multiple PDK corners and interpreted WNS/TNS metrics.  

---

## 📅 Week 4 — CMOS Power Supply & Device Variation Robustness

| Task | Description | Status |
|------|-------------|--------|
| [**Task 1**](Week4#-task-1--mosfet-behavior-the-current-voltage-chronicles) | 🔌 Simulate NMOS device, sweep Vds for different Vgs, plot Id vs Vds | ✅ Done |
| [**Task 2**](Week4#-task-2--threshold-voltage--velocity-saturation-the-speed-demons) | 📈 Sweep Vgs vs Id, extract threshold voltage Vt, observe velocity saturation | ✅ Done |
| [**Task 3**](Week4#-task-3--the-vtc-quest-finding-the-perfect-balance-point) | 🖥 Build CMOS inverter, sweep Vin, plot Vout vs Vin, identify switching threshold Vm | ✅ Done |
| [**Task 4**](Week4#-task-4--transient-response-when-time-becomes-critical) | ⏱ Apply pulse input, extract rise/fall propagation delays | ✅ Done |
| [**Task 5**](Week4#-task-5--noise-margins-the-robustness-test) | 🛡 Determine VIL, VIH, VOL, VOH from VTC, compute noise margins | ✅ Done |
| [**Task 6**](Week4#-task-6-cmos-power-supply--device-variation-robustness) | ⚡ Vary Vdd and transistor sizing, observe effect on VTC, switching point, noise margins, and delay | ✅ Done |

### 🌟 Key Learnings from Week 4

- Explored transistor-level behavior under voltage and sizing variations and linked device physics to timing constraints used in STA.

---

## 📅 Week 5 — OpenROAD Flow Setup & Floorplan + Placement

| Task | Description | Status |
|------|-------------|--------|
| [**Task 1**](Week5#-installation--execution-flow) | 📥 Clone OpenROAD flow scripts, run setup, and build tools | ✅ Done |
| [**Task 2**](Week5#-step-4%EF%B8%8F%E2%83%A3-verify-installation) | ✅ Verify installation using yosys and openroad | ✅ Done |
| [**Task 3**](Week5#-step-5%EF%B8%8F%E2%83%A3-execute-floorplan--placement-%EF%B8%8F) | 📐 Execute Floorplan and Placement (stop before routing) | ✅ Done |
| [**Task 4**](Week5#-step-6%EF%B8%8F%E2%83%A3-visualize-results-in-gui-%EF%B8%8F) | 👁️ Launch GUI to visualize floorplan and placed standard cells | ✅ Done |

### 🌟 Key Learnings from Week 5

- Transitioned from transistor-level SPICE to physical backend implementation using OpenROAD.  
- Understood how floorplanning defines chip boundaries and how placement affects timing and congestion.

---

## 📅 Week 6 — OpenLANE RTL-to-GDSII Flow

| Task | Description | Status |
|------|-------------|--------|
| [**Task 1**](Week6#-day-1--foundation-of-open-source-silicon) | 🏗️ OpenLANE workflow setup, Sky130 PDK fundamentals | ✅ Done |
| [**Task 2**](Week6#-day-2--floorplanning-fundamentals) | 📐 Floorplan configuration, die/core planning, library cell placement strategies | ✅ Done |
| [**Task 3**](Week6#-day-3--library-cell-design--characterization) | 🎨 Custom CMOS inverter design in Magic, SPICE extraction, timing characterization, and LEF generation | ✅ Done |
| [**Task 4**](Week6#-day-4--custom-cell-integration--sta) | ⏱️ Custom cell integration, pre-layout STA, slack optimization, CTS | ✅ Done |
| [**Task 5**](Week6#-day-5--pdn-routing--gdsii-sign-off) | 🛣️ PDN generation, routing, and final GDSII sign-off | ✅ Done |

### 🌟 Key Learnings from Week 6

- Mastered the OpenLANE automated RTL-to-GDSII flow from synthesis to sign-off using Sky130 PDK.  
- Designed and characterized a custom CMOS inverter cell and integrated it into the flow via LEF/LEF merging.  
- Optimized timing via synthesis strategies, sizing, and CTS and generated DRC-clean routing and GDSII.

---

## 📅 Week 7 — VSDBabySoc Physical Design & Post-Route Parasitic Extraction

| Task | Description | Status |
|------|-------------|--------|
| [**Task 1**]|🔧 OpenROAD-flow-scripts installation, VSDBabySoC file organization, and RTL synthesis with Yosys | ✅ Done |
| [**Task 2**]|	📐 Floorplan execution with macro placement for analog blocks (PLL & DAC) |	✅ Done |
| [**Task 3**]|	📍 Global and detailed placement with density heat map analysis and legalization | ✅ Done |
| [**Task 4**]|	⏰ Clock Tree Synthesis achieving 0.65ns skew, timing closure (WNS=5.55ns), and power analysis |	✅ Done |
| [**Task 5**]|	🛣️ Global and detailed routing with zero DRC violations for clean layout |	✅ Done |
| [**Task 6**]|	📊 Post-route SPEF (Standard Parasitic Exchange Format) generation for accurate timing sign-off | ✅ Done |

### 🌟 Key Learnings from Week 7

- Executed complete OpenROAD physical design flow for VSDBabySoC from synthesis to GDSII with analog macro integration.
- Fixed Liberty file power pin syntax (pg_pin) for PLL/DAC macros to enable proper OpenROAD parsing.
- Achieved timing closure (WNS=5.55ns, TNS=0ns) with optimized CTS reducing clock skew to 0.65ns.
- Completed zero-violation routing and generated post-route SPEF for accurate parasitic extraction.
- Learned pre-route vs post-route STA accuracy - SPEF-based analysis reduces timing error from ~30% to <5%.

---


## 🙏 Acknowledgment

I am thankful to [**Kunal Ghosh**](https://github.com/kunalg123) and Team **[VLSI System Design (VSD)](https://vsdiat.vlsisystemdesign.com/)** for the opportunity to participate in the ongoing **RISC-V SoC Tapeout Program**.  

I also acknowledge the support of **RISC-V International**, **India Semiconductor Mission (ISM)**, **VLSI Society of India (VSI)**, and [**Efabless**](https://github.com/efabless) for making this initiative possible.

---

## 📈 Weekly Progress Tracker

[![Week0](https://img.shields.io/badge/📦_Week_0-Tools_Setup-00C853?style=for-the-badge)](Week0)
[![Week1](https://img.shields.io/badge/⚡_Week_1-RTL_GLS-00C853?style=for-the-badge)](Week1/README.md)
[![Week2](https://img.shields.io/badge/🔧_Week_2-SoC_SDBaby-00C853?style=for-the-badge)](Week2/README.md)
[![Week3](https://img.shields.io/badge/⏱️_Week_3-SoC_STA-00C853?style=for-the-badge)](Week3/README.md)
[![Week4](https://img.shields.io/badge/🔬_Week_4-CMOS_Spice-00C853?style=for-the-badge)](Week4/README.md)
[![Week5](https://img.shields.io/badge/🛣️_Week_5-OpenROAD-00C853?style=for-the-badge)](Week5/README.md)
[![Week6](https://img.shields.io/badge/⚡_Week_6-OpenLANE_GDSII-00C853?style=for-the-badge)](Week6/README.md)

---

**Author**: Sneha Srivastava — [@srivastavasneha004](https://github.com/srivastavasneha004)


