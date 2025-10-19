# Week 4 — MOSFETs, VTC, Transient Response & Robustness

## Overview
This week explores device-level behavior and how it affects circuit performance. You will run SPICE experiments on CMOS inverters and single-transistor tests to extract Id‑Vds/Id‑Vgs curves, Voltage Transfer Characteristics (VTC), transient response (rise/fall times and propagation delay), noise margins, and study the effect of supply/device variation.

## Objectives
- Measure MOSFET Id‑Vds and Id‑Vgs characteristics.
- Extract threshold voltage (Vt) and observe velocity‑saturation effects for short channels.
- Build an inverter, sweep input to get the VTC and find the switching point (Vm).
- Run transient simulations to measure tr, tf, tPLH, tPHL and compute tP and fmax.
- Compute noise margins (VIL, VIH, VOH, VOL) and study robustness under supply/device variations.

## Tools
- ngspice (or your preferred SPICE)
- SkyWater 130nm SPICE models (Sky130 PDK files)
- Standard text editor and plotting tools (gnuplot/Matplotlib) for figures

## Tasks (summary)

### Task 1 — MOSFET Id‑Vds and Id‑Vgs
- Run DC sweeps on single NMOS/PMOS devices using Sky130 models.
- Produce Id vs Vds families for several Vgs values and Id vs Vgs transfer curves.
- Deliverables: `Images/` figures (Id‑Vds, Id‑Vgs), one‑page `MOSFET_Notes.pdf` summarizing observations.

Example SPICE (Id‑Vds sweep):
```
* NMOS Id-Vds sweep
.lib "sky130_fd_pr/models/sky130.lib.spice" tt
XM1 vdd out 0 0 sky130_fd_pr__nfet_01v8 w=0.39u l=0.15u
Vdd vdd 0 1.8
Vin in 0 DC 1.2
.dc Vdd 0 1.8 0.05
.control
  run
  plot -vdd#branch
.endc
```

### Task 2 — Threshold Extraction (Vt)
- Use transfer characteristics and the square‑root extrapolation method (√Id vs Vgs) to estimate threshold.
- Deliverable: `Vt_extraction.txt` and annotated plots in `Images/`.

### Task 3 — VTC of CMOS Inverter
- Create a minimum‑sized CMOS inverter (specify W/L for PMOS/NMOS). Sweep Vin from 0→VDD to get Vout vs Vin (VTC). Find Vm where Vout = Vin.
- Deliverables: `Images/Task3_invsout.png`, `VTC_results.txt` with Vm, VOH, VOL.

SPICE tip (VTC DC sweep):
```
.lib "sky130_fd_pr/models/sky130.lib.spice" tt
* Inverter netlist
.dc Vin 0 1.8 0.01
.control
  run
  plot v(out) vs v(in)
.endc
```

### Task 4 — Transient Response (tr, tf, delays)
- Apply a pulse input (with short edges) and run a transient simulation. Measure rise/fall times and propagation delays using `.measure` commands.
- Deliverables: `Images/Task4_Trans_in_out.png`, `timing_measures.txt` with tPLH, tPHL, tr, tf, tP, estimated fmax.

Example pulse source:
```
* Vin in 0 PULSE(0 1.8 0 1n 1n 10n 20n)
```

### Task 5 — Noise Margins
- From the VTC, compute VIL and VIH where |dVout/dVin| = 1 and then NM_L = VIL − VOL, NM_H = VOH − VIH.
- Deliverables: `Images/Task5_invsout.png`, `noise_margins.txt`.

### Task 6 — Supply & Device Variation Robustness
- Sweep VDD (e.g., 1.8 → 0.8 V) and/or vary transistor widths to study Vm migration and noise margin collapse.
- Deliverables: plots showing trends (`Images/Task6_waveform_diff_supp.png`, `Images/Task6_device_size_var.png`) and a short `Robustness_Observations.txt`.

## Where to put files
- Put plots/screenshots into `Week 4/Images/` (already present).
- Put reports/notes into `Week 4/` (e.g., `VTC_results.txt`, `noise_margins.txt`).
- Final submission PDF: `Week 4/Task/Week-4-Tasks-<your-id>.pdf` 

## How to run (quick commands)
1. Run DC/transfer simulations with ngspice:
```
ngspice <netlist.sp>
```
2. Run transient simulation and save plots with built‑in plotting or export raw data for Python.
3. Annotate figures and place them in `Images/`.

## Deliverables checklist
- [ ] Id‑Vds / Id‑Vgs plots (Images)
- [ ] Vt extraction (text + image)
- [ ] VTC plot and Vm value
- [ ] Transient waveform and timing measures
- [ ] Noise margins calculation
- [ ] Robustness analysis plots and notes
- [ ] Final report PDF in `Week 4/Task/`

## Author
Sneha Srivastava

## References
- SkyWater PDK & model files (Sky130)
- ngspice manual
