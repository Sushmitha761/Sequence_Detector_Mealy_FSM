# Sequence Detector Using Mealy Finite State Machine

## Introduction
In this design, I am going to detect the sequence “0001111 ” using Mealy finite state machine. Mealy finite state machine is used for faster generation of output, Mealy will be faster, in the sense that output will change as soon as an input transition occurs

---

# Description

A sequence detector is a digital sequential circuit that recognizes a predefined sequence of binary inputs. In a Mealy FSM, the output depends on both the current input and the present state, allowing the output to change immediately after the required input sequence is received.

The FSM moves through different states based on the incoming bits. Once the complete sequence is detected, the output signal becomes high for one clock cycle. This design demonstrates the complete RTL-to-GLS verification flow using open-source EDA tools.
A sequence detector is a sequential state machine. It produces a pulse output whenever it detects a predefined sequence. In case of Mealy machine, output is a function of not only the present inputs but also past inputs. In other words, we can say; in Mealy, both output and the next state depends on the present input and the present state. Here I have implemented the Mealy finite state machine sequence detector “101011”.


---

# Applications

- Digital Communication Systems
- Serial Pattern Detection
- Data Transmission Monitoring
- Barcode Readers
- Embedded Control Systems
- Protocol Verification
# Melay Machine Block Diagram

<img width="713" height="303" alt="image" src="https://github.com/user-attachments/assets/a09880bc-5b93-4bc8-9e5e-a4999600245b" />


---

# Software Requirements

- Verilog HDL
- Icarus Verilog
- GTKWave
- Yosys

---

# Functional Simulation

## Installation

```bash
sudo apt update
sudo apt install git
sudo apt install iverilog
sudo apt install gtkwave
```

## Simulation Commands

```bash
iverilog -o sim rtl/sequence_detector.v tb/tb.v
vvp sim
gtkwave dump.vcd
```

### Functional Simulation Result

The RTL design was compiled and executed successfully. The generated waveform confirmed that the sequence detector responded correctly to the applied input patterns.


<img width="946" height="622" alt="rtlsequence_detector v gtkwave" src="https://github.com/user-attachments/assets/b815b3cb-2b22-47d7-8fed-0de4ac5b6305" />

---

# RTL Synthesis

## About Yosys

Yosys is an open-source synthesis framework used to convert RTL Verilog code into an optimized gate-level netlist. The generated netlist is later used for Gate Level Simulation.

## Synthesis Commands

```tcl
read_verilog rtl/sequence_detector.v
synth -top sequence_detector
write_verilog sequence_detector_netlist.v
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

### Synthesis Result

The RTL design was synthesized successfully and a gate-level netlist was generated without synthesis errors.

<img width="925" height="462" alt="synthesizednetlist" src="https://github.com/user-attachments/assets/912a7fd9-78fd-42bf-a7c4-7c20b6f9a0eb" />

### Statistics
<img width="498" height="438" alt="Cell Statistics" src="https://github.com/user-attachments/assets/bd42e5d8-85e5-43b2-81e9-b65afefc668d" />


---

# Gate Level Simulation (GLS)

Gate Level Simulation verifies the synthesized netlist by applying the same testbench used for RTL simulation. This confirms the correctness of the synthesized hardware implementation.

## GLS Commands

```bash
iverilog -o gls_sim sequence_detector_netlist.v tb/tb.v
vvp gls_sim
gtkwave dump.vcd
```

### GLS Result

The synthesized netlist was simulated successfully. The generated waveform verified that the synthesized design behaved correctly under the given test conditions.
<img width="946" height="622" alt="Glswaveform" src="https://github.com/user-attachments/assets/5845f2ac-1543-4e5b-b4fe-91e66f554c59" />



---

# Observation

The Functional Simulation verified the RTL implementation successfully. After synthesis, the generated netlist was validated through Gate Level Simulation using the same testbench. The waveforms observed in GTKWave confirmed the correct functionality of the design throughout the verification flow. The complete design process, including RTL simulation, synthesis, and GLS, was completed successfully.

---

# Conclusion
The Mealy FSM based sequence detector was successfully designed, synthesized, and verified using Verilog HDL. Functional Simulation validated the RTL design, while Gate Level Simulation confirmed the correctness of the synthesized netlist. This project demonstrates the complete digital IC design flow using open-source tools such as Icarus Verilog, GTKWave, and Yosys.

---

