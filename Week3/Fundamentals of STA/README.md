# 🧠 Fundamentals of Static Timing Analysis (STA)

## 📘 Overview

Static Timing Analysis (STA) is a crucial step in digital circuit verification that ensures a design meets its timing requirements without needing simulation vectors.
It checks whether all data paths meet setup and hold time constraints, ensuring reliable operation across all process, voltage, and temperature (PVT) corners.

---

## 🧩 Table of Contents

- Timing Path
- Arrival Time and Slack
- Expected Time
- Types of Timing Analysis
- Slew / Transition Analysis
- Load Analysis
- Clock Analysis
- Timing Graph Model
- Analysis Methods
- Setup and Hold Verification
- Latches and Flip-Flops
- Jitter and Uncertainty
- On-Chip Variation (OCV)
- Process Variations
- Clock Effects

---

## 1. Timing Path

A timing path is the logical route a signal takes from a start point to an endpoint.

- Start Points: Flip-flop clock pins or input ports
- End Points: Flip-flop data (D) pins or output ports

### 🧮 Example Path Types

- Register to Register (reg2reg)
- Input to Register (in2reg)
- Register to Output (reg2out)
- Input to Output (in2out)

## 2. Arrival Time and Slack

- **Actual Arrival Time (AAT):** Time when a signal actually reaches its endpoint.
- **Required Arrival Time (RAT):** Latest time by which the signal must arrive for proper operation.

### 📏 Slack Formula

Slack = RAT − AAT

- Positive Slack: Timing is met ✅
- Negative Slack: Timing violation ⚠️

## 3. Expected Time

Defines target arrival times for signals at endpoints.

- **Setup (Max Delay):** Latest data arrival before next clock edge
- **Hold (Min Delay):** Minimum time data must remain stable after clock edge

## 4. Types of Timing Analysis

### 4.1 Setup and Hold Path Categories

| Type   | Description                                 |
|--------|---------------------------------------------|
| reg2reg| Between two flip-flops (launch → capture)   |
| in2reg | Input port → Flip-flop D pin                |
| reg2out| Flip-flop output → Output port              |
| in2out | Input port → Output port                    |

### 4.2 Other Timing Analyses

- **Clock Gating:** Verifies no glitches occur when enabling/disabling clocks.
- **Recovery/Removal:** For asynchronous reset/preset signals.
	- Recovery Time: Reset inactive before clock edge
	- Removal Time: Reset active after clock edge
- **Latch Timing (Time Borrowing):** Latches can “borrow” time when transparent.

## 5. Slew / Transition Analysis

Slew measures how quickly a signal transitions from one logic level to another.

- **Data Slew:** Transition rate of data signals
- **Clock Slew:** Transition rate of clock signals

⚠️ Excessive slew → slower logic, higher power, and degraded timing.

## 6. Load Analysis

Verifies whether drivers meet electrical limits.

- **Fanout:** Number of loads driven
- **Capacitance:** Total load on a signal line

Goal: Ensure load is within library-specified limits for accurate delay estimation.

## 7. Clock Analysis

### 7.1 Clock Skew

Skew = Capture Clock Latency − Launch Clock Latency

Clock skew affects setup and hold margins.

### 7.2 Pulse Width

Duration of clock’s HIGH or LOW phase.
Must meet minimum pulse width requirements for correct sequential logic operation.

## 8. Timing Graph Model

STA tools represent the circuit as a Directed Acyclic Graph (DAG) — also called a Timing Graph.

- **Nodes:** Pins or nets
- **Edges:** Timing arcs with delays

### 🧮 Calculation Flow

- **AAT (Actual Arrival Time):** Computed forward from sources
- **RAT (Required Arrival Time):** Computed backward from endpoints
- **Slack:** Slack = RAT − AAT

AAT should always be ≤ RAT for successful timing closure.

## 9. Analysis Methods

| Method | Description                                                   |
|--------|---------------------------------------------------------------|
| PBA    | Path-Based Analysis — accurate, follows exact physical path    |
| GBA    | Graph-Based Analysis — approximate, pessimistic but faster     |

## 10. Setup and Hold Verification

### 10.1 Setup Check

Ensures data arrives before the capture clock edge.

Combinational Delay < Clock Period − Setup Time

### 10.2 Hold Check

Ensures data remains stable after the clock edge.

Combinational Delay > Hold Time

## 11. Latches and Flip-Flops

| Element        | Function                                           |
|----------------|----------------------------------------------------|
| Positive Latch | Passes input to output when clock is HIGH          |
| Negative Latch | Passes input to output when clock is LOW           |
| Flip-Flop      | Combines master (negative latch) and slave stage   |

### 🧩 Timing Parameters

- **Setup Time:** Data must be stable before clock edge
- **Hold Time:** Data must remain stable after clock edge
- **CLK→Q Delay:** Propagation time from clock edge to Q output

## 12. Jitter and Uncertainty

**Jitter:** Random variation in clock edge timing (visualized in eye diagrams).

**Noise Margin:** Tolerance to noise/distortion.

**Uncertainty:** Extra timing margin added to account for jitter and variations.

## 13. On-Chip Variation (OCV)

Differences in voltage and ground potential across a chip cause delay variation.

- **Voltage Droop:** Temporary voltage reduction during switching.
- **Ground Bounce:** Ground potential fluctuation due to return currents.

### 🧮 OCV Derates

- **Max Derate:** Adds delay (used for setup checks)
- **Min Derate:** Reduces delay (used for hold checks)

## 14. Process Variations

Manufacturing variations affect transistor characteristics and path delays.

### 14.1 Sources of Variation

- **Etching Process:** Alters resistance and capacitance
- **Oxide Thickness:** Changes threshold voltage → delay variation

## 15. Clock Effects

- **Clock Pull-In:** Clock arrives earlier → reduced delay
- **Clock Push-Out:** Clock arrives later → increased delay

### 15.1 Pessimism and Removal

STA assumes worst-case conditions (max skew, jitter, OCV).
Pessimism Removal reduces over-conservative margins to better match real silicon performance.

---

## 🧾 Summary

Static Timing Analysis ensures that:

- All timing paths meet setup and hold constraints.
- No path violates clock, load, or slew specifications.
- Circuit functions correctly at the intended clock frequency across all PVT corners.

---

## ✍️ Author

**Sneha Srivastava**  
Project: Week 3 – Fundamentals of Static Timing Analysis
Date: October 11, 2025
