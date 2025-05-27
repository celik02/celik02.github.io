---
title: "MPC-Based Vehicle Overtaking Controller"
excerpt: "This project benchmarks PID, LQR, and MPC controllers for autonomous highway overtaking using a nonlinear bicycle model in the CARLA simulator.<br/><img src='/images/overtaking.png'>"
collection: portfolio
---

## Overview
This project investigates three control strategies—PID, LQR, and MPC—for the safety-critical task of highway overtaking in autonomous vehicles. Using a nonlinear bicycle-kinematic model in the CARLA simulator, we compare performance across tracking accuracy, energy use, comfort, and maneuver time.

**GitHub:** [github.com/celik02/oc_project](https://github.com/celik02/oc_project)

---

## Approach

1. **PID Controller**
   - Cascaded lateral/longitudinal loops tracking a precomputed waypoint trajectory
   - Model-free; tuned gains to balance stability vs. responsiveness

2. **LQR Controller**
   - Linearized bicycle model around the reference path
   - Gain-scheduled cost matrices for “straight” vs. “lane-change” phases

3. **MPC Controller**
   - Online optimization with CasADi over a 5 s horizon (Δt = 0.1 s)
   - Jointly plans steering and acceleration, enforces hard road and safety constraints

---

## Tools & Technologies
- **Simulation:** CARLA 0.9.15 (Town04 map)
- **Modeling & Control:** Python, CasADi
- **Sensors:**  GPS + IMU fusion (EKF)

---

## Key Results

| Metric                | PID      | LQR      | **MPC**     |
|-----------------------|----------|----------|-------------|
| Lateral RMS (m)       | 2.66     | 2.62     | **1.53**    |
| Speed RMS (m/s)       | **1.98** | 3.05     | 2.61        |
| Energy (kWh)          | **0.078**| 0.085    | 0.086       |
| Overtake Time (s)     | 19.8     | 19.5     | **12.0**    |
| Steering-rate (rad/s) | 8.00     | 2.48     | **0.45**    |

- **MPC** halved lateral error and cut maneuver time by ~40%, at a modest 10 % energy penalty.
- **PID** remains the most energy-efficient but struggles with coordinated lane-changes.

---

## Takeaways & Next Steps
- **Prediction Pays Off:** MPC’s horizon-based planning delivers smoother, more accurate overtakes.
- **Trade-offs:** Simple PID excels in efficiency; LQR offers balanced performance; MPC offers the best safety/time metrics.
- **Future Work:**
  1. Integrate an Extended Kalman Filter for real-time state estimation.
  2. Explore robust/adaptive MPC under varying traffic scenarios.
  3. Deploy controllers on a physical testbed to close the simulation-reality gap.