# UART Communication Protocol in Verilog

This repository contains a complete implementation of the **UART (Universal Asynchronous Receiver/Transmitter)** protocol using **Verilog HDL**, featuring a fully functional **Transmitter (UART_Tx)** and **Receiver (UART_Rx)**.  
The design uses a simple and efficient timing-based approach with a configurable baud timing parameter (`CLKS_PER_BIT`).  
Both modules are verified through simulation for correct serial communication, bit timing, and protocol accuracy.

---

## 🚀 Features

### ✅ **UART Transmitter (UART_Tx)**
- Parallel 8-bit input → serial output conversion  
- Generates:
  - **Start bit (0)**
  - **8 data bits (LSB first)**
  - **Stop bit (1)**
- Uses a **10-bit shift register** `{stop, data[7:0], start}`
- Bit timing based on `CLKS_PER_BIT` (default = 16)
- `busy` flag indicates transmission in progress
- Clean FSM-less, counter-based architecture

---

### ✅ **UART Receiver (UART_Rx)**
- Detects falling edge on `Rx` line → identifies **start bit**
- Waits half-bit period to sample in the center of each bit
- Samples all **8 data bits** LSB-first
- Packs received bits into a shift register
- Asserts `ready = 1` when a full byte is received
- Automatically returns to IDLE state for next frame
- Timing controlled using `CLKS_PER_BIT` counter

---
## 🧪 Simulation Overview

Your testbench (recommended):

- Sends parallel data byte to **UART_Tx**
- TX serializes the data frame  
- RX samples the incoming waveform  
- `ready = 1` asserts when RX reconstructs same byte  
- Waveforms confirm:
  - Start bit detection  
  - Mid-bit sampling  
  - Accurate bit timing  
  - Clean stop bit  
  - Reliable TX→RX operation  

---

## 🔧 Tools Used

- Verilog HDL  
- ModelSim / Vivado Simulator  
- FPGA RTL verification practices  

---

## 🎯 Project Purpose

This design is ideal for:

- FPGA beginners learning UART  
- Students implementing serial communication in HDL  
- RTL engineers practicing protocol design  
- Embedded system developers needing UART IP  
- Digital design interview preparation  
