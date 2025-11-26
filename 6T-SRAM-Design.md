# Design and Implementation of a 6T SRAM Cell (45nm) Using Cadence Virtuoso
### Overview

This project focuses on the complete design, simulation, and layout implementation of a 6-Transistor Static Random Access Memory (6T SRAM) cell using the 45nm CMOS technology node in Cadence Virtuoso.
The objective of this work is to design a compact, low-power, and stable memory bit-cell with reliable read/write functionality and robust Static Noise Margin (SNM).

At 45nm technology, SRAM becomes extremely sensitive to supply voltage variations, leakage, short-channel effects, and device mismatch. Hence, careful transistor sizing, optimized bit-cell architecture, and accurate verification through simulations are essential.

### Project Objectives

To design a 6T SRAM bit-cell using 45nm CMOS transistors in Cadence Virtuoso.

To analyze read, write, and hold operations through transient simulations.

To extract butterfly curves and evaluate Static Noise Margin (SNM).

To create a DRC-clean and LVS-matched layout of the SRAM cell.

To perform post-layout simulations incorporating parasitic effects.

To verify cell stability under different operating voltages and load conditions.

### Theoretical Background
#### SRAM Fundamentals

Static RAM (SRAM) is a type of volatile semiconductor memory used in cache, register files, and high-speed buffers. Unlike DRAM, SRAM does not require periodic refresh because data is stored using bistable latch circuits.

#### 6T SRAM Architecture

A 6T SRAM cell consists of:

Two cross-coupled inverters forming a stable latch.

Two NMOS pass (access) transistors connected to BL and BLB.

Word Line (WL) controlling access transistors.

Bit Line (BL) and Bit Line Bar (BLB) for reading and writing data.

#### Operations
(a) Hold Operation

WL = 0

Access transistors are OFF.

Cross-coupled inverters maintain the stored value.

(b) Write Operation

WL = 1

One of the bit lines is forced to '0' while the other is held at '1'.

The inverter pair flips to store the new value.

(c) Read Operation

BL and BLB precharged high.

WL = 1, one of the bit lines discharges slightly depending on the stored data.

Sense amplifier detects this differential voltage.

#### Design Constraints (45nm)

Read Stability requires keeping inverter NMOS strong and access transistor weak.

Write Ability requires access transistor stronger than pull-up PMOS.

Device Mismatch becomes significant due to short-channel effects.

Leakage power increases drastically at lower technology nodes.

### Schematic Design and Components
#### Components Used

2 PMOS transistors (pull-up devices)

2 NMOS transistors (pull-down devices)

2 NMOS pass transistors (word-line controlled access devices)

Technology: 45nm CMOS PDK

Supply Voltage: VDD = 1V (typical for 45nm)

#### Schematic Description

The two inverters are cross-connected to create bistability.

Access NMOS transistors connect internal storage nodes to BL and BLB.

The sizing followed the typical 45nm ratio:

Pull-down NMOS > Access NMOS > Pull-up PMOS

Ensures stable read and adequate write-margin.

<img width="1920" height="1080" alt="schematic" src="https://github.com/user-attachments/assets/2d64ac19-0438-46ae-927d-8c10ee64943f" />

#### Design Ratio Considerations

Read Stability Ratio:

<img width="164" height="95" alt="Screenshot From 2025-11-27 01-21-02" src="https://github.com/user-attachments/assets/da85f8b0-a0bf-46e5-a408-4a235c125581" />​

 must be sufficiently high.

Write Margin Ratio:

<img width="152" height="98" alt="Screenshot From 2025-11-27 01-21-09" src="https://github.com/user-attachments/assets/c60b53ef-ef8c-4c5c-bacc-097aeea2b5f4" />
	​
 
 must be greater to ensure flipping.

### Simulation Results
<img width="1920" height="1013" alt="schematic_new" src="https://github.com/user-attachments/assets/68c037e7-d60d-4a27-96ca-b106e32ca138" />

#### Transient Simulation – Write Operation

WL is asserted high.

BL/BLB are driven with differential inputs.

Storage nodes switch correctly between logical 0 and 1.

Write delay evaluated at 45nm is shorter due to low capacitance.

#### Transient Simulation – Read Operation

BL/BLB precharged to VDD.

WL enabled, causing slight discharge in one bit line.

Read SNM verified using butterfly curves.

No read-upset observed for selected transistor ratios.

#### Static Noise Margin (SNM)

Butterfly curve generated through inverter voltage transfer characteristics (VTC).

SNM_hold and SNM_read extracted.

Typically, SNM reduces during read operation due to voltage division at the storage node.

#### Power and Stability Observations

Leakage power significant at 45nm; optimized with proper device sizing.

Fail-safe operation confirmed for supply voltages between 0.8V to 1.2V.

Read/Write access times recorded in the order of tens of ps.


### Conclusion

The design and implementation of the 6T SRAM cell using 45nm CMOS technology was successfully carried out in Cadence Virtuoso.
The results show that the SRAM bit-cell:

Performs stable read/write/hold operations

Exhibits acceptable noise margins

Meets design constraints for low-voltage operation

Has a compact and verified layout (DRC & LVS compliant)

This work forms a fundamental building block for designing larger SRAM arrays, memory compilers, and cache subsystems in advanced VLSI design.
