# GLS of BabySoC — Post-Synthesis Gate-Level Simulation

VSD RISC-V Tapeout Program — Week 3 Assignment

## Purpose of GLS

Gate-Level Simulation (GLS) verifies the functionality of a design after synthesis. GLS runs on the synthesized gate-level netlist and (optionally) uses Standard Delay Format (SDF) annotations to exercise real gate delays. GLS checks whether the design behaves correctly with technology-mapped cells and timing information.

### Why GLS matters for BabySoC
- Confirms correct logic after synthesis and mapping to standard cells
- Verifies interactions between key modules (RISC-V CPU, PLL, DAC)
- Detects issues such as timing failures, metastability, or glitches that may not appear in RTL simulation

---

## Tools used
- Yosys (synthesis)
- Icarus Verilog (iverilog) or compatible gate-level simulator
- GTKWave (waveform viewer)

---

## Step-by-step GLS flow (commands)

Below are the commands and notes to run a typical post-synthesis GLS for `vsdbabysoc`.

1) Read Verilog sources and supporting modules (inside Yosys):

```tcl
read_verilog -sv -I src/include/ -I src/module/ \
	src/module/vsdbabysoc.v \
	src/module/clk_gate.v \
	src/module/rvmyth.v

# or load each file separately if preferred
read_verilog -I src/include/ src/module/vsdbabysoc.v src/module/rvmyth.v
read_verilog -I src/include/ src/module/clk_gate.v
```

2) Load cell libraries required for mapping and timing:

```tcl
read_liberty -lib src/lib/avsddac.lib
read_liberty -lib src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```

3) Synthesis and mapping to technology library:

```tcl
synth -top vsdbabysoc
read_liberty -lib src/lib/avsdpll.lib
dfflibmap -liberty src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
opt
abc -liberty src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib -script +strash;scorr;ifraig;retime;{D};strash;dch,-f;map,-M,1,{D}
```

Notes: the `abc` command above runs mapping/optimization passes; adapt the script to your Yosys/ABC version.

4) Final cleanup and flattening (recommended):

```tcl
flatten
setundef -zero
clean -purge
rename -enumerate
```

5) Write synthesized netlist to disk:

```tcl
write_verilog -noattr output/synth/vsdbabysoc.synth.v
```

6) Prepare simulation files (bring in library models and primitives), then compile and run gate-level simulation:

```bash
# copy/verilog models if not already present
cp -r ~/VSDBabySoC/my_lib/verilog_model/sky130_fd_sc_hd.v .
cp -r ~/VSDBabySoC/my_lib/verilog_model/primitives.v .

# ensure synthesized netlist and testbench are in expected paths
cp -r ~/VSDBabySoC/output/post_synth_sim/ ~/VSDBabySoC/src/module/

# compile gate-level simulation binary
iverilog -o ../../output/post_synth_sim/post_synth.out \
	-DPOST_SYNTH_SIM -DFUNCTIONAL -DUNIT_DELAY='#1' \
	-I ../include ../../output/synth/vsdbabysoc.synth.v ./sky130_fd_sc_hd.v ./primitives.v ./testbench.v

# run simulation
./post_synth_sim.out

# open GTKWave (example)
gtkwave output/post_synth_sim/post_synth_sim.vcd
```

7) Waveform review

Open the generated `.vcd` in GTKWave and inspect key signals (CLK, reset, CPU outputs, DAC outputs, important internal nets). Example waveform used in this report: `Images/Screenshot 2025-10-07 224631.png` (add this file to `Images/` if not present).

---

## Notes & Troubleshooting
- If simulation fails due to missing primitives, ensure `sky130_fd_sc_hd.v` and `primitives.v` are present and compatible with the simulator.
- For timing-accurate GLS, annotate the DUT with SDF (if you have SDF files): use `-S` or `sdf_annotate` depending on your simulator.
- If testbench paths or includes fail, verify relative paths or use absolute paths inside the container/environment.

---

## Author

Sneha Srivastava
Week 3 — Post-Synthesis GLS

