# ⏱️ Timing Graphs using OpenSTA

## Introduction

Static Timing Analysis (STA) is a deterministic method to verify whether a digital design meets timing requirements across all PVT corners without applying input vectors. OpenSTA is an open-source STA engine that provides a TCL-based interface for loading libraries, gate-level netlists, constraints, and reporting timing metrics (WNS, TNS, worst slacks, etc.).

This README shows common OpenSTA workflows: inline commands, SPEF-based timing, and running a TCL script for min/max timing across corners. Example commands assume you are running inside the OpenSTA shell (prompt `%`).

---

## Installation (Docker)

1. Clone the OpenSTA repository:

```bash
 git clone https://github.com/parallaxsw/OpenSTA.git
cd OpenSTA
```

2. Build the Docker image (Ubuntu 22.04 example):

```bash
sudo docker build --file Dockerfile.ubuntu22.04 --tag opensta .
```

3. Run the container (mount your home so you can access files):

```bash
sudo docker run -it -v "$HOME":/data opensta
```

Inside the container you'll get the OpenSTA prompt registered as `%`.

---

## Quick Inline Timing Flow (OpenSTA shell)

Run these commands at the OpenSTA prompt to perform a simple timing check:

```tcl
read_liberty /OpenSTA/examples/nangate45_slow.lib.gz
read_verilog /OpenSTA/examples/example1.v
link_design top
create_clock -name clk -period 10 {clk1 clk2 clk3}
set_input_delay -clock clk 0 {in1 in2}
report_checks
```

Notes:
- `report_checks` by default reports setup (max-delay) paths.
- To include hold (min-delay) paths, run:

```tcl
report_checks -path_delay min
```

---

## Yosys -> OpenSTA quick example

If you synthesize with Yosys, these are typical commands for a small example design:

```bash
cd ~/VSDBabySoC/OpenSTA/examples/
yosys
read_liberty -lib nangate45_slow.lib
read_verilog example1.v
synth -top top
show
```

`show` opens a visualization of the synthesized netlist (requires Graphviz).

---

## SPEF-based Timing (post-layout parasitics)

If you have SPEF/DSPEF parasitic files from extraction, include them for more accurate delay calculations:

```tcl
read_verilog /OpenSTA/examples/example1.v
link_design top
read_spef /OpenSTA/examples/example1.dspef
create_clock -name clk -period 10 {clk1 clk2 clk3}
set_input_delay -clock clk 0 {in1 in2}
report_checks
```

SPEF-based analysis gives more realistic slack and power estimates when post-layout RC is available.

---

## Automating with a TCL script (min/max delays)

Create a script `min_max_delays.tcl` with:

```tcl
# Load liberty files for max and min analysis
read_liberty -max /data/VSDBabySoC/OpenSTA/examples/nangate45_slow.lib.gz
read_liberty -min /data/VSDBabySoC/OpenSTA/examples/nangate45_fast.lib.gz

# Read the gate-level Verilog netlist
read_verilog /data/VSDBabySoC/OpenSTA/examples/example1.v

# Link the top-level design
link_design top

# Define clocks and input delays
create_clock -name clk -period 10 {clk1 clk2 clk3}
set_input_delay -clock clk 0 {in1 in2}

# Generate a full min/max timing report
report_checks -path_delay min_max > /data/VSDBabySoC/OpenSTA/examples/min_max_report.txt
report_wns -digits 4 > /data/VSDBabySoC/OpenSTA/examples/sta_wns.txt
report_tns -digits 4 > /data/VSDBabySoC/OpenSTA/examples/sta_tns.txt
report_worst_slack -max -digits 4 > /data/VSDBabySoC/OpenSTA/examples/sta_worst_max_slack.txt
report_worst_slack -min -digits 4 > /data/VSDBabySoC/OpenSTA/examples/sta_worst_min_slack.txt
```

Run inside OpenSTA with:

```tcl
source /data/VSDBabySoC/OpenSTA/examples/min_max_delays.tcl
```

---

 ## Visualizations and Plots

 Place generated plots (WNS/TNS, slack histograms, path diagrams) in the `Images/` folder and link them here. Example images in this repository:

 - `Images/flow.png` — flow diagram
 - `Images/opensta.png` — OpenSTA screenshot
 - `Images/paths.png` — example timing path
 - `Images/Task1_Pre_Post_simualtionCompare.png` — pre vs post synthesis waveform comparison

 You can view them directly from GitHub by clicking the file links.

 ---

 ## Tips & Troubleshooting

 - If OpenSTA reports "library already exists" or parsing errors, ensure Liberty files use `/* ... */` comments (Liberty does not accept `//` comments).
 - For path or file errors, double-check `read_verilog` and `read_liberty` paths and mount points when using Docker.
 - Use absolute paths when running inside the container and bind-mount the host directories with `-v "$HOME":/data`.

 ---

 ## References

- OpenSTA: https://github.com/parallaxsw/OpenSTA
- Example flows and tutorials referenced in Week 3 materials



 
