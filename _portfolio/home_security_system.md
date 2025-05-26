---
title: "Home Security System"
excerpt: "Home Security System<br/><img src='/images/home_security_system.png'>"
collection: portfolio
---
## Overview

The Home Security Project is an end-to-end, AI-driven monitoring system built around an NVIDIA Jetson Nano that delivers real-time intrusion detection, identity recognition, and remote control—all for under \$200 in hardware. Stereo CSI and ESP32-CAM modules capture video streams, while PIR sensors trigger motion-based alerts and guide active pan-tilt adjustments. On-board inference pipelines (MultiCue + YOLOv4-Tiny + dlib embeddings) classify individuals as Residents, Visitors, or Intruders, logging events locally and pushing snapshots and logs to Google Drive for off-site review. A companion mobile app (MIT App Inventor) provides live notifications, camera control, and event history, enabling homeowners to securely monitor and manage their property from anywhere.


<figure>
  <img src='/images/home_security_high_res.JPG' style="width: 70%; max-width: 700px; height: auto;">
  <!-- <figcaption>Figure: Block diagram of the overall system and data flow.</figcaption> -->
</figure>

## Components

- **Central Computer**
  NVIDIA Jetson Nano Developer Kit (2 GB RAM) running all decision and inference algorithms

- **Wired Camera**
  Raspberry Pi 4 CSI Camera Module (1080p @ 30 FPS) connected via the Jetson’s CSI port

- **Wireless Cameras**
  Two ESP32-CAM modules (5 V, up to 10 m range) each mounted on a pan-tilt servo assembly for adjustable field-of-view

- **Motion Sensors**
  Two HC-SR501 PIR sensors (7 m range, 120° detection cone) for motion triggering

- **Pan-Tilt & Servo Motors**
  Hobby servos driven by ESP32-CAM GPIO for remote camera aiming

---

## Subsystems

<figure>
  <img src='/images/data_flow_home_security_.png' style="width: 70%; max-width: 700px; height: auto;">
  <figcaption>Figure: Block diagram of the overall system and data flow.</figcaption>
</figure>

### 1. Sensor Subsystem
Acquires raw data from cameras and motion detectors:

- **Wired & Wireless Cameras** capture live video streams.

- **PIR Sensors** detect movement and cue the cameras.
- **Pan-Tilt Assembly** (servos + brackets) enables active FOV control.

### 2. Decision Subsystem
Processes sensor inputs and classifies each event:

- **Movement Detection** via background-subtraction (MultiCue) to trigger heavier processing
- **Object & Face Detection** using YOLOv4-Tiny for real-time localization of humans and pets
- **Face Recognition** with dlib-based 128-dim embeddings (via face_recognition API) for identity matching
- **Classification Logic** implements flowchart rules to label **Residents**, **Visitors**, **Suspects**, and **Intruders** based on database matches and behavior patterns
- **Database Management** stores face encodings, timestamped entry logs, and snapshots in a local SQLite database

### 3. User Interface Subsystem
Allows residents to monitor, control, and review events:

- **Mobile App** built with MIT App Inventor provides:
  - Real-time **notifications** of anomalies or intrusions
  - Remote **pan-tilt control** of wireless cameras
  - **Log browsing** and manual tagging of new faces
- Communication over the home’s common Wi-Fi network

### 4. Outer Structure Subsystem
Encloses and mounts all hardware:

- **3D-printed PLA Casings & Racks** for Jetson Nano, CSI camera, ESP32-CAM platform, USB camera, and PIR sensors
- Designs produced in **Catia** and **FreeCAD** for weatherproofing and aesthetic integration

---

## Technologies Used

- **Hardware**:
  Jetson Nano, Raspberry Pi CSI Camera, ESP32-CAM, HC-SR501 PIR, hobby servos, FTDI.

- **Algorithms & Libraries**:
  MultiCue BGS for motion detection; YOLOv4-Tiny for object/face detection; dlib & face_recognition for face matching.

- **Software & Tools**:
  Python, OpenCV, NVIDIA TensorRT optimizations; MIT App Inventor.

- **Interfaces & Protocols**:
  CSI, GPIO, UART; Wi-Fi networking.
---

## Connectivity & Remote Access

- **Google Drive Integration**
  A Python-based cloud storage automation module leverages the Google Drive API to upload captured snapshots, database backups, and event logs to a shared Drive folder—enabling off-site review and archival
