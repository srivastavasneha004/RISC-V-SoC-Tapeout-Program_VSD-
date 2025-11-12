## 🧠 Week 3 Task – Post-Synthesis GLS & STA Fundamentals

### 🎯 Objective
The goal of this week’s task is to:

- Perform Gate-Level Simulation (GLS) after synthesis to validate post‑synthesis functionality.
- Understand the fundamentals of Static Timing Analysis (STA) and perform basic timing checks using OpenSTA.
- Generate and interpret timing graphs to identify setup/hold violations and analyze slack.

---

### 🧩 Part 1 – Post‑Synthesis GLS

**Objective:** Verify that the synthesized design behaves functionally the same as the RTL (Week 2 functional simulation).

**Reference:** GLS Reference – VSD_HDP: Day 6

**Steps**
1. Perform Synthesis (Yosys) and generate the synthesized netlist and logs (`synth.log`).
2. Run Gate‑Level Simulation (GLS) using the synthesized netlist with a gate‑level testbench (Icarus Verilog / iverilog).
3. Compare GLS waveform with RTL functional waveform — they should match for functional correctness.

**Deliverables**
- `synth.log` — synthesis log files
- `gls_waveform.png` — GLS simulation waveform screenshot (put in `Images/`)
- `GLS_vs_Functional_Notes.txt` — short note confirming GLS output = Functional output

---

### 🧮 Part 2 – Fundamentals of STA (Static Timing Analysis)

**Objective:** Learn STA concepts: setup/hold checks, slack, clock definitions, and path‑based analysis.

**Deliverable**
- `STA_KeyNotes.pdf` — one‑page summary with definitions and interpretations (setup, hold, slack, clock constraints, critical paths)

---

### ⚡ Part 3 – Generate Timing Graphs with OpenSTA

**Objective:** Perform STA using OpenSTA and visualize timing paths and slack.

**Steps**
1. Load netlist and constraints inside OpenSTA:

```tcl
read_verilog output/synth/vsdbabysoc.synth.v
read_liberty ./STA_OUTPUT/sky130_fd_sc_hd__tt_025C_1v80.lib
read_sdc ./vsdbabysoc_synthesis.sdc
link_design vsdbabysoc
```

2. Run timing checks and collect reports:

```tcl
report_checks -path_delay max -fields {slew capacitance delay slack} > ./STA_OUTPUT/sta_report_max.txt
report_checks -path_delay min -fields {slew capacitance delay slack} > ./STA_OUTPUT/sta_report_min.txt
report_wns -digits 4 > ./STA_OUTPUT/sta_wns.txt
report_tns -digits 4 > ./STA_OUTPUT/sta_tns.txt
report_worst_slack -max -digits 4 > ./STA_OUTPUT/sta_worst_max_slack.txt
report_worst_slack -min -digits 4 > ./STA_OUTPUT/sta_worst_min_slack.txt
```

3. Capture timing path screenshots and save plots in `Images/` (e.g. `timing_graph.png`, `WNS.png`, `TNS.png`).

**Deliverables**
- `opensta_script.tcl` — OpenSTA TCL script
- `timing_report.txt` — STA timing report output
- `timing_graph.png` — timing path/graph screenshot (with userid & timestamp)
- `Observations.txt` — notes on critical path and slack interpretation

---

📅 **Summary – By End of Week 3**
✅ Perform Gate-Level Simulation (GLS) and verify post-synthesis correctness.

✅ Understand STA fundamentals (setup/hold, slack, clock, and timing paths).

✅ Use OpenSTA to perform real-world timing analysis and interpret timing reports.

✍️ Author
Name: Sneha Srivastava

Project: Week 3 – Post-Synthesis GLS & STA Fundamentals

Tools Used: Yosys, Icarus Verilog, GTKWave, OpenSTA


