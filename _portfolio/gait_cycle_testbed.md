---
title: "Gait Cycle Testbed for Prosthetic Knee Simulation"
excerpt: "A hardware platform with regenerative circuitry and Arduino control that lets you run real gait-cycle data and capture energy during knee motion.<br/><img src='/images/top_prosthetic_knee.jpeg' style='width: 60%; max-width: 500px; height: auto;'>"
collection: portfolio
published: true
---

## Gait Cycle Testbed for Prosthetic Knee Simulation

**Overview**
Built a two-motor testbed to emulate human walking and prosthetic-knee dynamics. One motor replays prerecorded gait-cycle profiles (angle & torque), while the second motor provides adjustable resistance and regenerative braking to mimic prosthetic knee behavior.

<figure>
  <img src='/images/couple_motors_prosthetic_knee.jpeg' style="width: 70%; max-width: 700px; height: auto;">
  <figcaption>Figure: Coupled electric motors to mimic knee flexion and prosthetic knee behavior  </figcaption>
</figure>

### My Role & Contributions
- **Regenerative Circuit Design:** Developed and prototyped a braking circuit (LTspice → breadboard) to harvest energy during knee flexion/extension phases.
- **Arduino Control Firmware:** Wrote synchronized control code on an Arduino Uno to command both motors from gait-cycle datasets.
- **Closed-Loop Motor Control:** Integrated incremental encoders and implemented PID loops to accurately reproduce gait angle and torque profiles.
- **System Validation:** Loaded standard gait datasets, ran end-to-end tests, and analyzed kinematic and power metrics to verify performance.

### Technologies & Tools
- **Embedded & Control:** Arduino Uno, PID control, incremental encoders
- **Power Electronics:** Custom regenerative braking circuit, LTspice for simulation
- **Software:** C/C++ (Arduino)

