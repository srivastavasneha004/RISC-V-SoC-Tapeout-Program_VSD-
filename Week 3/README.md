# ⚡️ Gate-Level Simulation (GLS) & Static Timing Analysis (STA) — Week 3

This Week 3 folder documents post-synthesis verification for VSDBabySoC:
- Gate-Level Simulation (GLS) using synthesized netlist
- Static Timing Analysis (STA) using OpenSTA across PVT corners

Folders
- `Images/` — screenshots and plots (OpenSTA, timing graphs, flow diagrams)
- `STA_OUTPUT/` — raw STA outputs and per-lib reports
- `Task/` — submitted task PDFs (week3_Part1.pdf, Week3_part2.pdf, week3_Part3.pdf)

---

## ⚡️ Gate-Level Simulation (GLS) of BabySoC

### Purpose
GLS verifies functionality after synthesis using gate-level netlist and annotated delays (SDF). This captures gate delays and cell-specific timing behavior.

### Typical GLS Flow (commands summary)
```bash
# After synthesis & write_verilog
# 1. Compile gate-level testbench
iverilog -o output/post_synth_sim/post_synth_sim.out -DPOST_SYNTH_SIM -I ./output/src/include -I ./output/src/module ./output/src/module/testbench.v

# 2. Run simulation
./output/post_synth_sim/post_synth_sim.out

# 3. View waveforms
gtkwave output/post_synth_sim/post_synth_sim.vcd
```

### Snapshots (see `Images/`)
- `Task1_Pre_Post_simualtionCompare.png` — pre vs post synthesis waveform comparison
- `Task1_Post_simulation.png` — post-synthesis waveform

---

## ⏱️ Static Timing Analysis (STA) using OpenSTA

### Purpose
Static Timing Analysis checks setup/hold timing across all paths without vectors. It reports WNS (Worst Negative Slack), TNS (Total Negative Slack), and per-corner metrics.

### Typical OpenSTA flow (TCL)
```tcl
# Example commands inside OpenSTA
read_liberty -min ./STA_OUTPUT/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -max ./STA_OUTPUT/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog ./vsdbabysoc.synth.v
link_design vsdbabysoc
read_sdc ./vsdbabysoc_synthesis.sdc
check_setup
report_checks -path_delay min_max -digits 4 > ./STA_OUTPUT/sta_report.txt
report_wns -digits 4 > ./STA_OUTPUT/sta_wns.txt
report_tns -digits 4 > ./STA_OUTPUT/sta_tns.txt
report_worst_slack -max -digits 4 > ./STA_OUTPUT/sta_worst_max_slack.txt
report_worst_slack -min -digits 4 > ./STA_OUTPUT/sta_worst_min_slack.txt
```

### PVT corners
The provided `STA_OUTPUT/` directory contains min/max timing reports for multiple PVT corners (lib files are present as `.txt`).

### Visualizations (in `Images/`)
- `WNS.png`, `TNS.png` — WNS/TNS plots
- `Worst_Setup_Slack.png`, `Worst_Hold_Slack.png` — slack visualizations
- `STA_All_Metrics.png` / `STA_AllMetrics.png` — combined metrics across corners
- `flow.png`, `opensta.png`, `paths.png` — flow and example path diagrams

---

## 📂 Files included (local)
- `Task/week3_Part1.pdf`
- `Task/Week3_part2.pdf`
- `Task/week3_Part3.pdf`
- `STA_OUTPUT/` — min/max lib reports, `sta_tns.txt`, `sta_wns.txt`, `sta_worst_*` files
- `Images/` — multiple plots and diagrams

---

## 🔧 Notes & Troubleshooting
- If OpenSTA reports "library already exists" or parsing errors, check Liberty file syntax (use /* ... */ for comments, not //).
- For path issues, verify the `read_verilog` path points to the synthesized netlist (`vsdbabysoc.synth.v`).

---

## 🧾 Summary
Week 3 covers post-synthesis verification (GLS) and timing validation (STA). The included reports and images summarize timing metrics across PVT corners and compare pre/post synthesis behavior.

---



