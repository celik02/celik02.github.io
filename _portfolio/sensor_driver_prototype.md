---
title: "Continuous Alcohol Monitoring Sensor Prototype"
excerpt: "Proof-of-concept analog front-end and bare-metal firmware for an in-house continuous alcohol sensor, enabling real-time data acquisition and visualization.<br/><img src='/images/sensor_drive_circuit.png'>"
collection: portfolio
---


## Project Overview
During my summer internship, I designed, built, and validated an amperometric driver circuit and bare metal firmware for a novel continuous alcohol sensor. This proof-of-concept demonstrates end-to-end data flow from chemical sensing through signal conditioning to live PC visualization, paving the way for a portable, low power continues alcohol monitoring device.
<figure>
  <img src='/images/sensor_drive_circuit.png' style="width: 70%; max-width: 600px; height: auto;">
</figure>


## Key Contributions
- **Circuit Design & Simulation**
  - Developed an amperometric analog front-end in LTSpice, optimizing gain, bandwidth, and noise performance for the target sensor chemistry.
  - Researched and selected low-power precision op-amps and bias components to maximize sensitivity and battery life.

- **Prototyping & Debugging**
  - Assembled the amplifier and bias network on a breadboard; procured and used an oscilloscope to verify DC operating points and transient response.
  - Iterated component values to align real-world measurements with simulation.

- **Firmware & Data Acquisition**
  - Wrote bare-metal C for the Nordic nRF52 MCU: configured the ADC, DMA, and UART peripherals for continuous sampling and streaming.
  - Implemented calibration routines and basic digital filtering to improve signal stability.

- **Data Visualization**
  - Built a Python (PySerial + Matplotlib) tool to ingest UART data, plot live sensor readings, and log to CSV for post-processing.

## Technologies & Tools
- **Hardware:** Nordic nRF52 (Arm Cortex-M4), precision op-amps, breadboard prototyping, oscilloscope
- **Software:** LTSpice, C (bare-metal), UART, Python (PySerial, Matplotlib)

---

> _This prototype laid the groundwork for miniaturized, battery-powered alcohol monitors capable of continuous, real-time readings in wearable and IoT applications._
