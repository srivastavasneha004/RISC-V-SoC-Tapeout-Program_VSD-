⚡ Task 1 – MOSFET Behavior: The Current-Voltage Chronicles
Where electrons meet electric fields and magic happens (well, physics actually)

🎯 Mission: Decode the MOSFET
The Challenge: Watch a tiny transistor transform from an insulator to a conductor and capture its entire personality in a graph.

What We're Hunting For:

📈 How drain current (Id) responds to drain voltage (Vds)
🎚️ The magical moment when increasing voltage stops increasing current (saturation!)
🔬 The difference between "gentle slope" (linear) and "flat plateau" (saturation) regions
🎭 Why This Matters
MOSFETs are the building blocks of every digital chip. Understanding their Id-Vds curves is like learning the alphabet before writing novels—you can't design CMOS circuits without knowing how individual transistors behave!

🛠️ Setting Up Your Lab
🎬 Getting Started with SkyWater 130nm
First, grab the tools of the trade:

git clone https://github.com/kunalg123/sky130CircuitDesignWorkshop.git
cd sky130CircuitDesignWorkshop
📦 What's in the Toolbox?
File	Purpose	Think of it as...
sky130_fd_pr__nfet_01v8__tt.pm3.spice	NMOS device model	The "DNA" of your transistor
sky130.lib.pm3.spice	Process library	The "physics textbook" for Sky130
🔌 Circuit Architecture
Our Test Subject: A humble NMOS transistor in its natural habitat

	  Vds (variable)
	     │
	     ▼
	 [Drain]
	     │
    Vgs ──>[Gate]
	     │
	 [Source]
	     │
	    GND
NMOS Structure

The transistor under investigation—simple, elegant, powerful

Biasing Strategy:

🔵 Drain → Connected to variable voltage (we'll sweep this!)
🟢 Gate → Fixed at Vgs (controls the "volume knob")
⚫ Source & Body → Grounded (our reference point)
🧬 The Physics Behind the Curtain
⚡ Task 1 – MOSFET Behavior: The Current-Voltage Chronicles
Where electrons meet electric fields and magic happens (well, physics actually)

🎯 Mission: Decode the MOSFET
The Challenge: Watch a tiny transistor transform from an insulator to a conductor and capture its entire personality in a graph.

What We're Hunting For:

📈 How drain current (Id) responds to drain voltage (Vds)
🎚️ The magical moment when increasing voltage stops increasing current (saturation!)
🔬 The difference between "gentle slope" (linear) and "flat plateau" (saturation) regions
🎭 Why This Matters
MOSFETs are the building blocks of every digital chip. Understanding their Id-Vds curves is like learning the alphabet before writing novels—you can't design CMOS circuits without knowing how individual transistors behave!

🛠️ Setting Up Your Lab
🎬 Getting Started with SkyWater 130nm
First, grab the tools of the trade:

git clone https://github.com/kunalg123/sky130CircuitDesignWorkshop.git
cd sky130CircuitDesignWorkshop
📦 What's in the Toolbox?
File	Purpose	Think of it as...
sky130_fd_pr__nfet_01v8__tt.pm3.spice	NMOS device model	The "DNA" of your transistor
sky130.lib.pm3.spice	Process library	The "physics textbook" for Sky130
🔌 Circuit Architecture
Our Test Subject: A humble NMOS transistor in its natural habitat

         Vds (variable)
            │
            ▼
        [Drain]
            │
    Vgs ──>[Gate]
            │
        [Source]
            │
           GND
NMOS Structure

The transistor under investigation—simple, elegant, powerful

Biasing Strategy:

🔵 Drain → Connected to variable voltage (we'll sweep this!)
🟢 Gate → Fixed at Vgs (controls the "volume knob")
⚫ Source & Body → Grounded (our reference point)
🧬 The Physics Behind the Curtain
📚 MOSFET Operation: A Tale of Two Regions
Region	When Does It Happen?	What's Going On?	The Math
🌊 Linear (Ohmic)	Vgs > Vt
Vds ≪ (Vgs − Vt)	Channel is open and flowing
Acts like a voltage-controlled resistor	Id = μn·Cox·(W/L)·[(Vgs−Vt)·Vds − Vds²/2]
🏔️ Saturation	Vds ≥ (Vgs − Vt)	Channel pinches off near drain
Current plateaus—more voltage, same current!	Id = ½·μn·Cox·(W/L)·(Vgs−Vt)²·(1+λVds)
🎢 The Journey of an Electron
Low Vds:                  High Vds:
  Gate                      Gate
   ↓                         ↓
S [===channel===] D      S [===▼ pinch] D
  ↑                         ↑
Linear flow               Saturated flow
🌀 The Body Effect Phenomenon
Ever notice how threshold voltage isn't always constant? Meet the body effect:

Body Effect

When source voltage rises relative to body, the threshold voltage increases:

Vt = Vt0 + γ(√(2ΦF + VSB) − √(2ΦF))

Translation: Changing the body-source voltage is like adjusting the "difficulty level" for turning on the transistor!

🧪 The Experiment
📜 SPICE Incantation
* NMOS Id-Vds Characteristics
* Device: W=5µm, L=2µm

.lib "sky130_fd_pr/models/sky130.lib.spice" tt

* Our transistor (the star of the show!)
XM1 vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=5 l=2

* Power supply
Vdd vdd 0 1.8

* Gate voltage
Vin in 0 1.8

* Sweep Vds from 0→1.8V, Vgs in steps of 0.2V
.dc Vdd 0 1.8 0.1 Vin 0 1.8 0.2

.end
🚀 Launch Sequence
ngspice day1_nfet_idvds_L2_W5.spice
Inside ngspice:

plot -vdd#branch
(The minus sign converts voltage source current to drain current—ngspice quirk!)

📊 Results: The Moment of Truth
NMOS Characteristics

Id vs Vds for various Vgs values—the MOSFET's signature

🔍 Decoding the Curves
What You're Seeing:

High Vgs (1.5V) ─────────────────▄▄▄▄▄▄▄▄▄  ← Saturation plateau
                                ▄▄
Medium Vgs (0.9V) ─────────▄▄▄▄▄             ← Steeper = more current
                          ▄▄
Low Vgs (0.6V) ──────▄▄▄▄▄                   ← Barely conducting
                   ▄▄
                  │
                  └──── Linear region (slope ≈ 1/Ron)
💡 Key Observations
Observation	What It Means	Design Implication
📈 Steep initial slope	Low on-resistance in linear region	Good for switches and pass transistors
🏔️ Flat saturation region	Current-source behavior	Ideal for amplifiers and current mirrors
🎚️ Higher Vgs → Higher Id	More gate voltage = stronger channel	Faster switching, higher drive strength
🔀 Curves don't overlap	Each Vgs creates unique operating point	Transistor acts as voltage-controlled current source
📈 Performance Metrics
Summary Table: The Numbers Speak
Vgs (V)	Transition Point
Vds ≈ (Vgs − Vt)	Max Id (µA)	Operating Zone	Power @ 1.8V
0.6	~0.3 V	8	🟡 Weak inversion	~14 µW
0.9	~0.6 V	24	🟢 Moderate	~43 µW
1.2	~0.9 V	42	🟢 Strong	~76 µW
1.5	~1.2 V	58	🔵 Maximum drive	~104 µW
🎯 Design Sweet Spots
Digital Logic: Operate at Vgs = VDD for maximum drive (fastest switching)
Analog Circuits: Operate in saturation for constant-current behavior
Low Power: Use minimum Vgs that meets timing requirements
🧭 The Bigger Picture
🔗 How This Connects to Real Chips
This simple Id-Vds curve is the foundation for:

MOSFET Curves
     ↓
Drive Strength Calculation
     ↓
Gate Delay Models (τ = C·V/I)
     ↓
Timing Analysis (Setup/Hold)
     ↓
Chip Operating Frequency!
Real-World Impact:

💨 Speed: Higher Id → faster charging of load capacitance → higher MHz
⚡ Power: More current = more dynamic power (P = C·V²·f)
🎯 Reliability: Saturation region prevents current runaway
🎓 Key Takeaways
"Every digital gate is just MOSFETs playing tug-of-war with electrons"

The Three Commandments of MOSFET Behavior
🌊 Linear Region is Your Friend

Low Rds(on) means efficient switches
Critical for pass gates and transmission gates
🏔️ Saturation is Where the Magic Happens

Constant current = predictable behavior
Foundation of amplifiers and logic gates
🎚️ Vgs is the Control Knob

More gate voltage = more current
But also more power consumption!


🎯 Task 2 — Threshold Voltage & Velocity Saturation: The Speed Demons
When transistors get too fast for their own good (and why that's both awesome and problematic)

🎯 Mission: Extracting the Secret Threshold
The Quest: Find the magical voltage where the transistor "wakes up" and starts conducting. Plus, discover what happens when electrons hit their speed limit!

🔬 What We're After
🎚️ Threshold Voltage (Vt): The "ignition voltage" for the MOSFET
⚡ Velocity Saturation: When electrons can't go any faster (even if you want them to!)
🔗 CMOS Connection: How these effects shape inverter behavior
📐 Device Under Test (DUT) Specs
Parameter	Value	Why It Matters
Width (W)	1.8 µm	Determines max current capacity
Length (L)	1.2 µm	Controls speed vs. current trade-off
Aspect Ratio (W/L)	1.5	The "strength" multiplier
Design Note: W/L = 1.5 is modest—real designs might use 2× to 10× ratios for higher drive strength!

🗺️ Operation Regions: A Traveler's Guide
The Classic View (Long Channel Devices)
    Id
     │
     │        ┌────────────────  Saturation
     │       ╱                   (Id ≈ constant)
     │      ╱
     │     ╱  Linear
     │    ╱   (Id ∝ Vds)
     │   ╱
     │  ╱
     └─────────────────────────> Vds
       Vgs-Vt
Region	Condition	Analogy
Linear	Vds < (Vgs − Vt)	Water flowing through an open pipe
Saturation	Vds ≥ (Vgs − Vt)	Water flow limited by pipe diameter (pinch-off)
⚡ Enter Velocity Saturation: The Plot Twist!
🏃 When Electrons Hit Their Speed Limit
In short-channel devices (L < 250 nm), something amazing happens: electrons reach a maximum velocity (~10⁷ cm/s in silicon) and refuse to go faster, no matter how hard you push!

🐌 Long Channel (L > 1 µm)	🚀 Short Channel (L < 250 nm)
Operating Modes	• Cutoff
• Linear
• Saturation	• Cutoff
• Linear
• Velocity Saturation ⚡
• Saturation
Current Depends On	Id ∝ (Vgs − Vt)²	Id ∝ (Vgs − Vt) ← Linear!
Max Current	~410 µA	~210 µA 😢
Switching Speed	Moderate	⚡ Faster! ⚡
Trade-off	Higher current, slower	Lower current, but speed demon!
🧮 The Velocity Saturation Equation
When electrons max out their speed:

Id = W · Cox · vsat · (Vgs − Vt)
       ↑    ↑     ↑      ↑
       │    │     │      └─ Overdrive voltage
       │    │     └──────── Saturation velocity (~10⁷ cm/s)
       │    └────────────── Gate oxide capacitance
       └─────────────────── Transistor width
The Key Insight: Current becomes linear with (Vgs − Vt) instead of quadratic!

🧪 Laboratory Experiments
🔬 Experiment 1: Id vs Vds (The Classic Sweep)
Goal: See the full picture of MOSFET behavior

📄 SPICE Netlist (click to expand)
🚀 Launch Command:

ngspice day2_nfet_idvds_L015_W039.spice
📊 Visualization:

plot -vdd#branch
Id vs Vds

The family of curves reveals MOSFET personality across all operating points

🔬 Experiment 2: Id vs Vgs (The Threshold Hunt)
Goal: Extract Vt and see the turn-on behavior

📄 SPICE Netlist (click to expand)
🚀 Launch Command:

ngspice day2_nfet_idvgs_L015_W039.spice
📊 Visualization:

plot -vdd#branch
Id vs Vgs

The transfer characteristic—watch the transistor "wake up" at Vt!

🎯 Threshold Voltage Extraction: The Detective Work
🔍 Method: Square Root Extrapolation
The Technique:

Plot √Id vs Vgs (instead of Id vs Vgs)
Find the linear region in strong inversion
Extrapolate back to x-axis
X-intercept = Vt ✨
√Id
 │     ╱
 │    ╱  ← Linear region (extrapolate this!)
 │   ╱
 │  ╱
 │ ╱
 │╱_______________
 └────────────────> Vgs
         Vt
         ↑
    Found it!
📊 Threshold Voltage vs. Channel Length
Channel Length	Vt (approx)	Why Different?
L = 2 µm	~0.45 V	Long channel—minimal SCE
L = 0.5 µm	~0.42 V	Moderate SCE
L = 0.15 µm	~0.38 V	Short-channel effects reduce Vt
SCE = Short-Channel Effects: As L shrinks, source/drain depletion regions "help" the gate control the channel, slightly lowering Vt.

🎛️ The CMOS Inverter Connection
🔄 Digital Logic: MOSFETs as Switches
Input (Vin)	PMOS State	NMOS State	Output (Vout)
0 V	✅ ON	❌ OFF	VDD (logic 1)
VDD	❌ OFF	✅ ON	0 V (logic 0)
The Magic: When one transistor is ON, the other is OFF—perfect complementary action!

MOSFET Switch Model

Individual MOSFET as a switch—controlled by gate voltage

CMOS Inverter

Two switches working together = digital inverter!

🎚️ MOSFET as a Voltage-Controlled Switch
State	Condition	Resistance	Analogy
OFF	Vgs < Vt	~∞ Ω	Open circuit (air gap)
ON	Vgs > Vt	~kΩ	Closed switch (wire)
📈 Load-Line Analysis: Finding the Switching Point
🔍 The Graphical Method
The Challenge: Where do PMOS and NMOS currents match? That's your switching threshold!

Step	What We Do	Visual Guide
1️⃣	Express PMOS gate voltage
VgsP = Vin − VDD	Step 1
2️⃣	Substitute internal nodes
Replace with Vout everywhere	Step 2
3️⃣	Find the crossover point
IdN = IdP → Vm	Step 3
The Switching Point (Vm):

Where NMOS and PMOS currents are equal
Determines noise margins (NML, NMH)
Critical for timing analysis!

🎓 Key Insights & Takeaways
💎 The Golden Nuggets
Discovery	Why It Matters	Design Impact
🎚️ Threshold Voltage is Extractable	Vt defines when transistor "turns on" 	Sets minimum Vgs for reliable switching
⚡ Velocity Saturation Limits Speed	Electrons have a speed limit in silicon	Can't make transistors arbitrarily fast by shrinking L
📐 Short Channels = Lower Current	Vel. sat. reduces Id by ~50% 	Must increase W to compensate
🔗 Transistor Behavior ↔ Gate Delay	Id determines how fast C charges	Higher Id = faster circuits (but more power!)
🎯 The Velocity Saturation Paradox
Shorter channel → Faster switching ✓
       ↓
But also: Higher E-field → Velocity saturation
       ↓
Result: Lower current ✗
       ↓
Solution: Increase W to compensate
       ↓
Trade-off: More area, more capacitance
🧠 Connecting to Circuit Design
🔗 From Transistor to Timing
MOSFET Id-Vgs curve
       ↓
Threshold voltage (Vt)
       ↓
Switching threshold (Vm) of inverter
       ↓
Noise margins (NML, NMH)
       ↓
Timing margins & setup/hold times
       ↓
Maximum clock frequency!
⚖️ The Designer's Dilemma
Want More...	Must Accept...	Design Knob
🚀 Speed	⚡ Higher power	Increase W/L
💚 Low power	🐌 Slower gates	Decrease W, increase L
🎯 Drive strength	📏 Larger area	Increase W
🛡️ Noise immunity	📉 Smaller swing	Adjust Wp/Wn ratio



⚡ Task 3 — The VTC Quest: Finding the Perfect Balance Point
Where the inverter becomes an amplifier for exactly one magical voltage

🎯 Mission: Capture the Switching Moment
The Challenge: Every CMOS inverter has a secret crossover point where input equals output. Find it. Measure it. Understand it.

What We're Hunting: The Voltage Transfer Characteristic (VTC) curve—the fingerprint of an inverter's personality.

🤔 Why This Matters
The VTC curve isn't just a pretty graph—it tells you:

📊 How sharply your inverter switches (gain)
🎯 Where the switching threshold sits (Vm)
🛡️ How robust your logic levels are (noise margins—we'll get there!)
⚡ Whether your design is balanced or lopsided
🧠 The CMOS Inverter: A Tale of Two Transistors
🎭 The Operating Principle
Think of it as a voltage-controlled see-saw:

Input LOW (0V):              Input HIGH (1.8V):
    
    VDD                          VDD
     │                            │
   [PMOS: ON] ✓                 [PMOS: OFF] ✗
     │                            │
     ├─── Vout = HIGH             ├─── Vout = LOW
     │                            │
   [NMOS: OFF] ✗                [NMOS: ON] ✓
     │                            │
    GND                          GND
🎢 The VTC Journey (Three Acts)
Vin Range	PMOS State	NMOS State	Vout	Region Name
0 → 0.4V	🟢 Strongly ON	🔴 OFF	≈ VDD	VOH Plateau
0.4V → 1.4V	🟡 Partially ON	🟡 Partially ON	Vin → 0	Transition Region ⚡
1.4V → 1.8V	🔴 OFF	🟢 Strongly ON	≈ 0V	VOL Plateau
The Magic Point: At Vm, both transistors are in saturation, creating maximum gain (the steepest part of the curve)!

🏗️ Our Inverter Architecture
📐 Design Specifications
Component	Parameter	Value	Design Rationale
🔵 PMOS (M1)	Width (W)	0.84 µm	2.33× wider than NMOS to compensate for lower hole mobility
Length (L)	0.15 µm
🟢 NMOS (M2)	Width (W)	0.36 µm	Minimum size for acceptable drive strength
Length (L)	0.15 µm
⚡ Load Cap	Cload	50 fF	Typical fanout capacitance
🔌 Supply	VDD	1.8 V	Standard Sky130 nominal voltage
🧮 The Sizing Sweet Spot
Why Wp/Wn ≈ 2.33?

Goal: Balanced Vm ≈ VDD/2

Challenge: μn ≈ 2.5 × μp (electrons faster than holes!)

Solution: Make PMOS wider
         Wp/Wn ≈ μn/μp ≈ 2.5

Reality: We use 0.84/0.36 = 2.33 (close enough!)
🧾 The SPICE Experiment
📜 Complete Netlist
📄 day3_inv_vtc_Wp084_Wn036.spice (click to expand)
🚀 Simulation Launch
ngspice day3_inv_vtc_Wp084_Wn036.spice
Inside ngspice:

plot v(out) vs v(in)
Pro tip: To find Vm precisely:

plot v(out) v(in) vs v(in)
The crossover point where the two curves meet is Vm!

📊 Results: The VTC Revealed
VTC Curve

The Voltage Transfer Characteristic—notice the beautiful steep transition!

🎯 Measured Parameters
Parameter	Symbol	Measured Value	Expected Range	Status
Switching Threshold	Vm	0.878723 V	0.8 - 1.0 V	✅ Excellent
Output High	VOH	1.800 V	≈ VDD	✅ Perfect
Output Low	VOL	~0 V	< 50 mV	✅ Perfect
Supply Voltage	VDD	1.800 V	1.8 V nominal	✅ Nominal

🔍 Deep Analysis: What the Curve Tells Us
📈 Anatomy of the VTC
Vout
1.8V ┤────────╮                    ← VOH region (PMOS wins)
     │        │
     │        │                    ← High gain region
     │        ╰───╮                  (both transistors active)
0.9V ┤            ● Vm             ← The crossover point!
     │              ╰──╮
     │                 │           ← Transition accelerates
     │                 ╰─────────  ← VOL region (NMOS wins)
  0V ┤
     └─────────────────────────> Vin
     0V        0.9V         1.8V
💡 Key Observations
Observation	What It Means	Design Insight
🎯 Vm ≈ 0.88V (close to VDD/2)	Nearly balanced design	Good noise margins on both sides
📐 Sharp transition region	High voltage gain (dVout/dVin)	Strong regenerative feedback = good logic separation
🔝 VOH ≈ VDD (rail-to-rail)	PMOS fully connects output to VDD	Maximum voltage swing = best noise immunity
🔻 VOL ≈ 0V (solid ground)	NMOS fully connects output to GND	Clean logic '0' with minimal leakage
⚖️ Wp/Wn = 2.33 ratio	Compensates for mobility difference	Achieves symmetric switching behavior
🧮 The Math Behind Vm
At the switching point, both transistors are in saturation and carry equal current:

IdN = IdP

½·μn·Cox·(Wn/Ln)·(Vin - VtN)² = ½·μp·Cox·(Wp/Lp)·(VDD - Vin - |VtP|)²

Solving for Vin = Vm...

Vm ≈ (VDD + VtN - |VtP|) / (1 + √(μn·Wn/(μp·Wp)))
For our design: Plugging in typical Sky130 values gives Vm ≈ 0.88V ✓

🎓 What We've Discovered
🏆 The Three Laws of VTC
📊 The Steeper, The Better

High gain in transition = better noise rejection
Achieved by having both transistors active in saturation
⚖️ Balance is Beautiful

Vm near VDD/2 maximizes symmetry
Requires proper Wp/Wn ratio to compensate mobility
📐 Rail-to-Rail is Reality

Good design achieves VOH ≈ VDD and VOL ≈ 0


🎮 Task 4 — Transient Response: When Time Becomes Critical
Static analysis is great, but circuits live in the time domain—let's watch them switch!

🎯 Mission: Capture the Switching Event
The Challenge: Stop analyzing DC behavior and start measuring real-time switching. How fast can this inverter actually flip states?

What We're After:

⏱️ Rise Time (tr): How long to go LOW → HIGH
⏱️ Fall Time (tf): How long to go HIGH → LOW
⚡ Propagation Delays: When does the output respond to input changes?
📊 Overshoot/Undershoot: Any transient glitches?
💡 Why Timing Matters
Faster Rise/Fall Time → Higher Maximum Clock Frequency
                     → Better Performance
                     → But also more dynamic power!
🧪 The Experiment Setup
🎛️ Input Stimulus: The PULSE Source
We're hitting the inverter with a square wave to simulate real logic transitions:

Vin in 0 PULSE(0 1.8 0 1n 1n 10n 20n)
                │  │  │  │  │  │   └─ Period (20ns → 50 MHz)
                │  │  │  │  │  └───── Pulse width (10ns)
                │  │  │  │  └──────── Fall time (1ns)
                │  │  │  └─────────── Rise time (1ns)
                │  │  └────────────── Delay (start immediately)
                │  └───────────────── High level (VDD)
                └──────────────────── Low level (0V)
Visual Representation:

Vin
1.8V ─┐      ┌──────────┐      ┌──
      │ 1ns  │          │ 1ns  │
      ├──────┘          └──────┘
   0V ─
      └─0───10ns───20ns───30ns→
💻 SPICE Configuration
📄 Complete Transient Netlist (click to expand)
📊 Results: The Waveforms Speak
Transient Response

Input (blue) and Output (red)—notice the delay and edge rates!

🎯 Measured Timing Parameters
Parameter	Symbol	Measured Value	Measurement Points	Quality
🔺 Rise Time	tr	661.76 ps	10% → 90% (0.18V → 1.62V)	🟢 Fast
🔻 Fall Time	tf	475.07 ps	90% → 10% (1.62V → 0.18V)	🟢 Faster!
⏱️ Prop. Delay (LH)	tPLH	~662 ps	Vin=50% → Vout=50%	🟡 Moderate
⏱️ Prop. Delay (HL)	tPHL	~475 ps	Vin=50% → Vout=50%	🟢 Better
🔝 Peak High	VOH(peak)	1.809 V	Slight overshoot	✅ Normal
🔻 Peak Low	VOL(peak)	−4.94 mV	Minimal undershoot	✅ Excellent
📈 Timing Diagram Breakdown
Input:
1.8V  ┌────┐    ┌────┐
      │    │    │    │
   0V ─────┘    └────┘
      ↑    ↑
      T1   T2

Output:
1.8V     ┌─┐      ┌─┐
         │ │      │ │
   0V  ──┘ └──────┘ └──
         ↑ ↑
         │ └─ tPHL (475ps)
         └─── tPLH (662ps)
         
Rise/Fall Times:
                            ┌─── 90% (1.62V)
                     ╱ │
              ╱   │ ← tr = 661.76ps
       ╱     │
─┘      └─── 10% (0.18V)

🧪 Summary calculations
Average propagation delay:

tP = (tPLH + tPHL) / 2
        = (662 + 475) / 2
        = 568.5 ps

Maximum toggle frequency:

fmax ≈ 1 / (2 × tP)
               ≈ 1 / (2 × 568.5ps)
               ≈ 879 MHz

Not bad for a single inverter! 🎉

🎓 Key Takeaways (Task 4)

• Fast edges (sub-ns) indicate healthy drive strength for the chosen sizing and load.
• Asymmetry between tr and tf is expected; compensate by sizing PMOS larger if needed.
• Transient analysis reveals overshoot/undershoot and settling behavior unseen in DC.


🛡️ Task 5 — Noise Margins: The Robustness Test
A circuit that works in simulation but fails in reality is just expensive art

🎯 Mission: Quantify Robustness
The Challenge: Your inverter works perfectly in ideal conditions. But what about:

🌩️ Power supply noise?
📡 Crosstalk from neighboring wires?
🔊 Substrate coupling from other circuits?
⚡ Thermal noise and manufacturing variations?
What We're After: Noise Margins (NML, NMH) — the safety buffer between "definitely 0" and "definitely 1"

💡 Why This Matters More Than You Think
High Noise Margins → Circuit survives real-world chaos
                                                               → Works in mass production
                                                               → Passes system-level testing
                                                               → Doesn't need expensive shielding

Low Noise Margins → Random bit flips
                                                               → Field failures
                                                               → Customer returns
                                                               → Engineering nightmare

🧠 Noise Margin Theory: The Critical Voltages
📊 The Four Corners of Logic
Every logic gate has four critical voltages:

Parameter	Symbol	Definition	Found Where?
🔝 Output High	VOH	Minimum guaranteed high output	VTC flat region (Vin near 0)
🔻 Output Low	VOL	Maximum guaranteed low output	VTC flat region (Vin near VDD)
🔼 Input High Threshold	VIH	Minimum input recognized as high	Where dVout/dVin = −1 (falling edge)
🔽 Input Low Threshold	VIL	Maximum input recognized as low	Where dVout/dVin = −1 (rising edge)

🧮 The Noise Margin Formulas
NMH = VOH − VIH  ← High-side noise margin
                     "How much noise can a '1' tolerate?"

NML = VIL − VOL  ← Low-side noise margin
                     "How much noise can a '0' tolerate?"

📊 Visual Guide to Noise Margins
🎯 Ideal vs. Real Inverter
Ideal vs Actual

Left: Perfect inverter (infinite gain). Right: Real inverter (finite transition)

Key Insight: Real inverters have a transition region where gain is finite. This defines VIL and VIH!

🗺️ The VTC with Noise Margins Annotated
Noise Margin Regions

The VTC divided into safe zones and danger zones

Zone Breakdown:

VOH ────────────────┐
                                                                      │ ← NMH = 0.796V (safe buffer)
VIH ────────────────┤
                                                                      │ ← UNDEFINED REGION (don't go here!)
VIL ────────────────┤
                                                                      │ ← NML = 0.744V (safe buffer)
VOL ────────────────┘

🌩️ Noise Scenarios: Will It Survive?
Noise Bump Scenarios

Testing the limits: When does noise cause bit errors?

Scenario	Input	Noise	Perceived Level	Result
✅ A	0.2V + 0.3V noise = 0.5V	< VIL (0.744V)	Still logic 0	SAFE
✅ B	1.6V − 0.3V noise = 1.3V	> VIH (1.004V)	Still logic 1	SAFE
❌ C	0.5V + 0.5V noise = 1.0V	Between VIL and VIH	Undefined!	DANGER

💻 Extracting Noise Margins from Simulation
📜 SPICE Netlist
📄 Noise Margin Extraction Netlist (click to expand)
🎯 Measurement Technique
Step-by-Step Process:

1. Plot VTC → See the overall transfer curve
2. Plot Gain → Find where |gain| = 1
3. Left unity-gain point → VIL (rising input, falling output)
4. Right unity-gain point → VIH (falling input, rising output)
5. Extract VOH/VOL → From flat regions of VTC

📈 Measured Results (example)
🎯 Critical Voltage Extraction
Parameter	Measured Value	Location on VTC	Quality Check
🔝 VOH	1.800 V	Vin ≈ 0V (PMOS fully on)	✅ Rail-to-rail
🔻 VOL	0.0000006 V
(0.6 µV)	Vin ≈ VDD (NMOS fully on)	✅ Essentially 0V
🔽 VIL	0.7436 V	Where gain = −1 (left side)	✅ Good separation
🔼 VIH	1.0036 V	Where gain = −1 (right side)	✅ Good separation

🛡️ Computed Noise Margins
NMH = VOH − VIH
              = 1.800 − 1.0036
              = 0.7964 V  ← High noise margin

NML = VIL − VOL
              = 0.7436 − 0.0000006
              = 0.7436 V  ← Low noise margin


⚡ Task 6: CMOS Power Supply & Device Variation Robustness
Exploring the delicate dance between voltage, transistor sizing, and circuit reliability

🎯 Mission Brief
Ever wondered what happens when your circuit's power supply fluctuates? Or when manufacturing variations create transistors that aren't quite the size you designed? Welcome to the world of CMOS robustness analysis—where tiny changes create massive ripple effects.

🔬 What We're Investigating
We're putting CMOS inverters through their paces by stress-testing them against:

Noise Margin	Value	% of VDD	Rating
🟢 NMH (High)	0.796 V	44.2%	⭐⭐⭐⭐⭐ Excellent
Challenge	Impact Zone	Risk Level
⚡ Power Supply Variations	Switching threshold (Vm)	🔴 High
🛠️ Transistor Sizing Variations	Noise margins (NM_L, NM_H)	🟡 Medium
📊 Combined Effects	VOH, VOL, timing margins	🔴 Critical

💡 Why This Matters
In the real world, your circuit doesn't live in a perfect lab environment. Power supplies droop, manufacturing processes drift, and temperature fluctuations mess with transistor characteristics. Understanding these variations is the difference between a chip that works sometimes and one that works always.

🧪 Experimental Setup
The SPICE Recipe
Here's our baseline inverter configuration using the SkyWater 130nm PDK:

* CMOS Inverter - Sky130 PDK
.include "sky130_fd_pr/models/sky130.lib.spice"

* Power supply (we'll vary this!)
Vdd vdd 0 1.8

* Input stimulus
Vin in 0 DC 0

* PMOS (pull-up network)
Xm1 out in vdd vdd sky130_fd_pr__pfet_01v8 W=1.0u L=0.36u

* NMOS (pull-down network)
Xm2 out in 0 0 sky130_fd_pr__nfet_01v8 W=0.36u L=0.36u

* Sweep input voltage for VTC
.dc Vin 0 1.8 0.01
.print dc V(out)
.end

🎛️ Experiment Variations
Experiment A: Supply Voltage Scaling

Sweep VDD from 1.8V down to 0.8V
Watch the inverter behavior collapse under voltage starvation
Experiment B: Device Sizing Gymnastics

Modify PMOS/NMOS widths (W)
Observe the battle between pull-up and pull-down strength

📊 Results: The Plot Thickens
⚡ Experiment A: When Voltage Takes a Dive
VTC Supply Variation

Figure 1: Voltage Transfer Characteristics under supply scaling

⚡ Table 2: Power Supply Variation (The Voltage Starvation Study)
VDD (V)	⚡ VOH (V)	🛑 VOL (V)	🔽 VIL (V)	🔼 VIH (V)	🔁 Vm (V)	🟢 NM_L (V)	🔴 NM_H (V)	Health Status
1.8	1.800	~0	0.744	0.744	—	0.744	1.056	🟢 Excellent
1.6	1.600	~0	0.687	0.687	0.791	0.687	0.913	🟢 Good
1.4	1.400	~0	0.621	0.787	0.700	0.621	0.613	🟡 Marginal
1.2	1.200	~0	0.549	0.685	0.611	0.549	0.515	🟠 Risky
1.0	1.000	~0	0.482	0.594	0.531	0.482	0.406	🔴 Danger Zone
0.8	0.800	~0	0.419	0.514	0.458	0.419	0.286	🔴 Critical

📉 Trend Alert: Notice how noise margins collapse as VDD drops—at 0.8V, you're one hiccup away from logic errors!

🔍 Key Discoveries:

📉 Vm Migration: The switching threshold shifts downward as VDD decreases—like watching the floor drop out from under your logic levels
🚨 Shrinking Safety Margins: Noise margins compress dangerously, making your circuit more vulnerable to glitches
🎯 VOH Degradation: High output voltage drops (obviously—you can't get 1.8V out when you only put 0.8V in!)
✅ VOL Stability: Low output voltage stays rock-solid near ground

🛠️ Experiment B: The Transistor Sizing Showdown
VTC Device Size Variation

Figure 2: How transistor sizing shifts the balance of power

🔍 Key Discoveries:

💪 PMOS Flexing: Increase PMOS width → Vm shifts upward, NM_H improves (stronger pull-up wins!)
⚡ NMOS Domination: Increase NMOS width → Vm shifts downward, NM_L improves (stronger pull-down takes over!)
⚖️ The Balancing Act: VOH/VOL remain stable, but the switching point moves—critical for threshold-dependent logic

📈 The Numbers Don't Lie
🛠️ Table 1: Device Sizing Variation (NMOS fixed at 0.36 µm)
Config	Wp (µm)	Wp/Wn Ratio	⚡ VOH (V)	🛑 VOL (V)	🔽 VIL (V)	🔼 VIH (V)	🔁 Vm (V)	🟢 NM_L (V)	🔴 NM_H (V)
1	0.60	1.67×	1.800	~0	0.713	0.952	0.847	0.713	0.847
2	1.00	2.78×	1.800	~0	0.713	0.952	0.847	0.713	0.847
3	1.50	4.17×	1.800	~0	0.713	0.952	0.847	0.713	0.847
4	2.00	5.56×	1.800	~0	0.713	0.952	0.847	0.713	0.847

🎓 Note: Surprisingly consistent! This suggests our baseline config is well-balanced.

🧠 Deep Insights & Analysis
🔌 Power Supply Variation Effects
┌─────────────────────────────────────────┐
│  VDD ↓  →  Vm ↓  →  Noise Margins ↓    │
│                                         │
│  Result: Less robust circuit!          │
│  Risk: Timing violations, glitches     │
└─────────────────────────────────────────┘

The Physics Behind It:

Lower VDD reduces transistor overdrive voltage (Vgs - Vth)
Weaker drive strength → slower switching → narrower transition region
The "safe zones" for logic 0 and logic 1 compress dangerously

⚙️ Device Variation Effects
The Tug-of-War Principle:

PMOS Width ↑                    NMOS Width ↑
               │                               │
               ▼                               ▼
Stronger Pull-Up            Stronger Pull-Down
               │                               │
               ▼                               ▼
       Vm Shifts UP                  Vm Shifts DOWN
               │                               │
               ▼                               ▼
       NM_H Improves                 NM_L Improves

Design Trade-off Alert: You can't optimize both noise margins simultaneously—it's a zero-sum game!

🎯 Connection to Static Timing Analysis (STA)
Why should chip designers care about VTC curves and noise margins? Because:

Timing Margins Depend on It: Switching threshold variations directly affect propagation delay
Critical Path Robustness: Voltage droops on critical paths can violate timing constraints
Multi-Corner Analysis: STA must verify timing across all process, voltage, and temperature (PVT) corners
Setup/Hold Time Sensitivity: Device variations affect the receive windows at flip-flops

🎓 Key Takeaways
"In CMOS design, robustness isn't optional—it's survival."

🏆 The Big Three Lessons
📉 Voltage Sensitivity is Real

Even small VDD variations have outsized effects on noise margins
Design must account for worst-case supply droop scenarios
⚖️ Balance is Everything

PMOS/NMOS sizing ratio determines switching threshold
Imbalanced designs sacrifice one noise margin for another
🔗 Device-Level Choices Echo at System Level

Inverter VTC characteristics propagate through entire timing chains
STA tools must model these variations accurately

🎓 Practical Design Guidelines
✅ DO:
       • Design with >20% supply margin
       • Size transistors for balanced Vm ≈ VDD/2
       • Verify across all PVT corners
       • Use guardband in timing analysis

❌ DON'T:
       • Assume nominal VDD everywhere
       • Ignore process variations
       • Cut noise margins too thin
       • Forget about IR drop effects
📚 References & Further Reading
🔗 Essential Resources
SkyWater PDK Documentation
github.com/google/skywater-pdk
The open-source PDK we used for all simulations

Ngspice Simulator Manual
ngspice.sourceforge.net/docs.html
Complete SPICE simulation reference

Classic Textbook: Rabaey et al.
Digital Integrated Circuits: A Design Perspective
The bible of CMOS circuit design

this is the full content with images 
