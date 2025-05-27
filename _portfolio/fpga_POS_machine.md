---
title: "FPGA POS Machine"
excerpt: "FPGA POS Machine<br/><img src='/images/pos_machine.png' style='width: 60%; max-width: 500px; height: auto;'>"
collection: portfolio
---

## FPGA-Based Point of Sale (POS) Terminal

### Overview
Design and implementation of a prototype POS machine on a Cyclone V FPGA using Verilog HDL. The system supports item selection, removal, and real-time total calculation, interfacing with an external monitor via VGA and providing user input through push buttons and switches.

### Key Features
- **Dual Operation Modes**
  - **Navigation Mode:** Visual menu navigation and product selection with 4-directional buttons and combination presses for “select”.
  - **Barcode Mode:** 4-digit barcode entry via push buttons; matching products are highlighted dynamically before quantity entry.
- **Item Management**
  - Add items by quantity entry; remove items by setting quantity to zero in deletion mode.
  - Automatic balance update in Turkish lira (TL) with four-digit display (ab.cd format).
- **VGA Integration**
  - 640×480 @60 Hz display of menu and cart using 8-bit color (3R,3G,2B) stored in ROM blocks.
  - Custom image pipeline: PNG→BMP→TXT→.tv, loaded into FPGA ROM for fast rendering.

### Technology Stack
- **Hardware:** Cyclone V FPGA, VGA port, push buttons, DIP switches
- **Languages & Tools:** Verilog HDL, Quartus, MATLAB (image conversion)
- **Memory Architecture:** Multiple ROM submodules for static image storage, optimized to reduce compilation time from 40 min to under 5 min.
- **Clock Management:** 25 MHz VGA clock derived from 50 MHz FPGA clock; 4 Hz debounced clock for button inputs.

### Highlights
- Optimized compilation by partitioning image ROM into four submodules, leveraging FPGA memory blocks instead of CLBs.
- Implemented pixel-level synchronization with front/back porches and sync pulses for reliable VGA timing.
- Developed Verilog routines to render 30×30 B/W digit matrices into on-screen boxes via `readmemb` and controlled `always` loops.

### Demo


<iframe width="560" height="315" src="https://www.youtube.com/embed/WcSQdT5mn8c" title="FPGA POS Machine Demo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

