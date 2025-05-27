---
title: "Milestone IP Integration"
excerpt: " Developed a modular Python library and PyQt5 GUI to seamlessly integrate real-time IP-based video streaming with Milestone’s VMS—overcoming SDK limitations by implementing custom SOAP/TCP messaging, JPEG frame parsing, and multithreaded decoding for low-latency playback.<br/><img src='/images/milestone_sdk.png'>"
collection: portfolio
---

**Technologies:** Python (Zeep, `requests`, `socket`, `threading`), WSDL/SOAP, TCP/IP (port 7563), XML, OpenCV (`cv2.imdecode`), PyQt5, JPEG marker parsing, Wireshark .

- **Integration Method Selection:**
  - Component integration with Milestone’s C# SDK failed due to hidden function bodies and Java incompatibility.
  - C++ SDK attempt was abandoned after unresolved dependency conflicts.
  - Chose IP protocol integration to gain full control by manually crafting messages.

- **Authentication & Configuration:**
  - Parsed WSDL services (SOAP actions) to perform HTTP-Basic login and retrieve a 4-hour authentication token via Python Zeep.
  - Called `Login` → `GetConfiguration` to extract camera GUIDs for downstream TCP connections.

- **TCP Socket Communication:**
  - Established a persistent TCP socket to Milestone’s Image Server on port 7563.
  - Constructed and sent `<connect>`, `<live>`, and `<stop>` XML messages by hand, adhering to Milestone’s IP protocol.

- **Real-Time Video Frame Extraction:**
  - Streamed continuous data blobs, identified JPEG SOI (`0xFFD8`)/EOI (`0xFFD9`) markers to segment individual frames.
  - Decoded each frame using OpenCV’s `imdecode` for display.

<figure>
  <img src='/images/jpeg_image.png' alt="GUI Design">
  <figcaption>Figure: JPEG Image Byte Array</figcaption>
</figure>


- **Concurrency for Low Latency:**
  - Used Python multithreading to separate network I/O, frame decoding, and GUI updates, preventing queue backlogs and ensuring smooth playback

- **GUI Development:**
  - Built a PyQt5 interface to input server IP, authenticate, list cameras, and control live video (play/stop).
  - Addressed thread cleanup and backlog issues when toggling the live stream

<figure>
  <img src='/images/aselsan_gui.png' alt="GUI Design">
  <figcaption>Figure: Simple GUI design to Display Video and Manage HTTP Communication</figcaption>
</figure>

**Outcome:**
Delivered a modular Python library and user-friendly GUI capable of real-time IP-based video.
