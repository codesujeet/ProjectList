# 🚗 ADAS Vehicle – Drive-By-Wire Autonomous System

> A Drive-By-Wire (DBW) enabled autonomous electric vehicle platform where steering, braking, and throttle are controlled electronically without mechanical linkages. Designed for real-time ADAS functionality with a focus on safety, reliability, and modularity.

---

## 📑 Table of Contents

- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Key Implementations](#key-implementations)
- [Technical Details](#technical-details)
- [System Workflow](#system-workflow)
- [Outcome](#outcome)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [License](#license)

---

## Overview

This project implements a full-stack autonomous driving pipeline on a Drive-By-Wire electric vehicle. The system replaces traditional mechanical linkages with electronic control of steering, braking, and throttle, enabling precise computer-controlled actuation. Multiple Advanced Driver Assistance System (ADAS) features operate concurrently in real-time to ensure safe and reliable autonomous navigation.

---

## System Architecture

The architecture follows a **layered modular approach**, enabling independent development and testing of each subsystem:

```
┌──────────────────────────────────────────────────────────────┐
│                     PERCEPTION LAYER                         │
│         Camera  +  Automotive RADAR (ARS 404-21)             │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│               FUSION & LOCALIZATION LAYER                    │
│       Sensor Fusion  │  Object Detection  │  Positioning     │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                    PLANNING LAYER                             │
│       Trajectory Generation  │  Decision Making              │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                    CONTROL LAYER                              │
│    Lateral Controller  │  Longitudinal Controller            │
│              Vehicle Actuation via CAN Bus                   │
└──────────────────────────────────────────────────────────────┘
```

| Layer                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------------ |
| **Perception**         | Camera + ARS 404-21 RADAR for environment sensing                  |
| **Fusion & Localization** | Sensor fusion for object detection and relative positioning     |
| **Planning**           | Trajectory generation and decision-making algorithms               |
| **Control**            | Lateral and longitudinal controllers for actuation via CAN bus     |

---

## Key Implementations

### 🟢 Adaptive Cruise Control (ACC)
- Maintains a safe following distance from the lead vehicle
- Uses RADAR data for distance and relative velocity measurements
- Dynamically adjusts throttle and braking to match traffic flow

### 🔴 Autonomous Emergency Braking (AEB)
- Real-time collision avoidance through object detection
- Time-to-collision (TTC) estimation for immediate threat assessment
- Automatic hard braking when collision is imminent

### 🟡 Lane Keep Assist (LKA)
- Vision-based lane detection using camera feed
- Real-time steering correction to keep the vehicle centered in the lane
- Handles curved and straight road segments

### 🔵 Path Following
- Trajectory tracking using closed-loop control algorithms
- Supports pre-defined paths and dynamically generated trajectories
- Smooth steering and speed transitions for passenger comfort

---

## Technical Details

| Component          | Specification                                          |
| ------------------ | ------------------------------------------------------ |
| **Compute**        | NVIDIA Jetson Nano                                     |
| **Communication**  | CAN Bus (real-time sensor-actuator interface)          |
| **RADAR**          | Continental ARS 404-21 (automotive-grade)              |
| **Control**        | Closed-loop control for steering and speed regulation  |
| **Speed Range**    | Designed for low-speed autonomous operation (~30 km/h) |
| **Actuation**      | Drive-By-Wire (electronic steering, braking, throttle) |

---

## System Workflow

```
    ┌─────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
    │ Sensors │────▶│  Fusion  │────▶│ Planning │────▶│ Control  │
    │(Camera, │     │& Object  │     │(Trajectory│    │(Steering,│
    │ RADAR)  │     │Detection)│     │  & Path)  │    │ Braking, │
    └─────────┘     └──────────┘     └──────────┘    │ Throttle)│
                                                      └────┬─────┘
                                                           │
                                                      ┌────▼─────┐
                                                      │ CAN Bus  │
                                                      │(Vehicle  │
                                                      │Actuation)│
                                                      └──────────┘
```

---

## Outcome

✅ Achieved **stable lane-following** and controlled navigation on test tracks  
✅ **Reliable actuator response** with real-time processing  
✅ Demonstrated all four ADAS features (ACC, AEB, LKA, Path Following) concurrently  
✅ Validated system performance under low-speed autonomous operation conditions  

---

## Getting Started

### Prerequisites
- NVIDIA Jetson Nano (with JetPack SDK)
- CAN Bus interface hardware
- Camera module (CSI/USB)
- Continental ARS 404-21 RADAR
- Drive-By-Wire compatible vehicle platform

### Setup
```bash
# Clone the repository
git clone <repository-url>
cd ADAS-Vehicle-DBW

# Install dependencies
pip install -r requirements.txt

# Configure CAN interface
sudo ip link set can0 up type can bitrate 500000

# Launch the ADAS system
python main.py
```

---

## Project Structure

```
ADAS-Vehicle-DBW/
├── perception/             # Camera and RADAR processing
│   ├── camera/             # Lane detection, object recognition
│   └── radar/              # RADAR data processing (ARS 404-21)
├── fusion/                 # Sensor fusion and localization
├── planning/               # Trajectory generation & decision making
├── control/                # Lateral & longitudinal controllers
│   ├── steering/           # Steering control algorithms
│   ├── braking/            # Braking control algorithms
│   └── throttle/           # Throttle control algorithms
├── can_interface/          # CAN Bus communication layer
├── adas_features/          # ADAS module implementations
│   ├── acc/                # Adaptive Cruise Control
│   ├── aeb/                # Autonomous Emergency Braking
│   ├── lka/                # Lane Keep Assist
│   └── path_following/     # Path Following
├── config/                 # Configuration files
├── tests/                  # Unit and integration tests
├── docs/                   # Documentation
├── requirements.txt
└── README.md
```

---

## License

This project is developed for academic and research purposes. Please refer to the `LICENSE` file for details.

---

<p align="center">
  <b>Built with precision for autonomous mobility 🏎️</b>
</p>
