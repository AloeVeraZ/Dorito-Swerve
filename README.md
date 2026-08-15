<div align="center">

# Dorito Kiwi Swerve Drivetrain

### A low-cost, 3-module holonomic swerve drivetrain with closed-loop continuous rotation steering

[![Status](https://img.shields.io/badge/Status-Active_Prototype-22c55e?style=flat-square)](#overview)
[![Kinematics](https://img.shields.io/badge/Kinematics-3--Module_Kiwi_Swerve-00aeef?style=flat-square)](#the-approach)
[![Control](https://img.shields.io/badge/Control-Closed--Loop_Python-8b5cf6?style=flat-square&logo=python&logoColor=white)](#electronics-and-control)
[![License](https://img.shields.io/badge/License-BSD_3--Clause-f59e0b?style=flat-square)](LICENSE)

<picture>
  <img src="docs/assets/dorito-prototype.jpg" alt="The Dorito Kiwi swerve drivetrain prototype" width="820" draggable="false">
</picture>

An experimental omnidirectional robot platform engineered with 3 symmetric modules, commercial off-the-shelf components, continuous-rotation servos, and real-time encoder feedback.

<strong>Quick navigation:</strong><br>
[Project Overview](#overview) | [Kinematic Architecture](#the-approach) | [Software Control](#electronics-and-control) | [Prototype Results](#prototype-results) | [Project Videos](#videos) | [Repository Files](#repository-contents)

</div>

---

## Overview

**Dorito** is an experimental omnidirectional robot drivetrain that explores a simpler and more accessible alternative to conventional four-module swerve systems: three symmetrically arranged modules, affordable general-purpose parts, continuous rotation servos for steering, and software-based closed-loop control.

The goal is a drivetrain that is competitive enough for competitive robotics, practical for assistive platforms, inexpensive to repair, and transparent for teaching mechanical design and feedback control.

| System Parameter | Technical Specification |
| --- | --- |
| Drivetrain geometry | 3-module symmetric Kiwi swerve (120° module spacing) |
| Steer actuation | High-torque continuous rotation servos |
| Steering feedback | 12-bit magnetic absolute rotary encoders |
| Drive transmission | HTD2 synchronous timing belts |
| Steer transmission | Heavy-duty HTD5 synchronous timing belts |
| Computing host | Raspberry Pi 4 running Python closed-loop kinematics |
| Power management | 10 A independent H-bridge drive channels + dedicated servo bus |

> [!NOTE]
> **Status:** Active prototype. Mechanical linkages, steering PID loops, and odometry integration are actively maintained and tested.

## The Approach

Dorito uses a **Kiwi swerve** configuration with three modules spaced symmetrically around the triangular chassis. Compared with a typical four-module system, this eliminates 25% of all actuators, drivers, and gearing while maintaining complete 3-DOF planar mobility:

- Omnidirectional translation (forward, backward, lateral, diagonal)
- Independent in-place rotation
- Simultaneous translation and rotational trajectory tracking

<table>
  <tr>
    <td align="center"><strong>Driver or Autonomous Command</strong></td>
    <td align="center">&rarr;</td>
    <td align="center"><strong>Python Kiwi Kinematics</strong></td>
    <td align="center">&rarr;</td>
    <td align="center"><strong>Module Velocity and Heading Targets</strong></td>
  </tr>
  <tr>
    <td align="center"><strong>12-Bit Absolute Encoders</strong></td>
    <td align="center">&rarr;</td>
    <td align="center"><strong>Closed-Loop Steering</strong></td>
    <td align="center">&rarr;</td>
    <td align="center"><strong>Servo HAT &rarr; Rotating Wheel Pods</strong></td>
  </tr>
  <tr>
    <td align="center"><strong>Velocity Targets</strong></td>
    <td align="center">&rarr;</td>
    <td align="center"><strong>10 A Motor Drivers</strong></td>
    <td align="center">&rarr;</td>
    <td align="center"><strong>Three Drive Motors &rarr; Wheel Pods</strong></td>
  </tr>
</table>

## Subsystem Architecture

### Mechanical Construction
- **Triangular Chassis:** Symmetric layout ensures equal weight distribution across all three contact patches.
- **Stationary Motors:** Drive motors and steering servos remain fixed to the chassis while wheel pods rotate 360° continuously.
- **Dual Timing Belts:** HTD5 belts absorb high steering shock loads; lightweight HTD2 belts deliver drive torque.
- **Hybrid Materials:** 3D-printed structural housings reinforced with CNC machined aluminum mounting plates.

### Electronics and Control
- **Raspberry Pi Host:** Computes inverse kinematics and steering vector resolution at high refresh rates.
- **12-Bit Encoders:** Provide absolute angular position feedback directly at each module pivot axis.
- **Current Scaling:** Software dynamically limits combined motor peak current to prevent battery voltage brownouts.

## Prototype Results

- **Complete 3-DOF Mobility:** Validated agile omnidirectional translation and continuous spin maneuvers.
- **Reduced Complexity:** 25% reduction in motor drivers, wiring bundles, and structural mass vs. 4-wheel swerve.
- **Precision Steering:** Continuous rotation servos paired with 12-bit encoders achieve tight angle tracking without mechanical stops.

## Videos

Click any preview to watch project demonstrations on YouTube:

| Full Project Breakdown | Prototype Steering Demo | Driving & Maneuverability |
| :---: | :---: | :---: |
| [![Full-length Dorito project explanation](docs/assets/demo-kinematics.webp)](https://www.youtube.com/watch?v=B4kNNsTJaLg) | [![Dorito prototype video 2](docs/assets/demo-steering.webp)](https://www.youtube.com/watch?v=usliYLL-PGs) | [![Dorito prototype video 3](docs/assets/demo-drive.webp)](https://www.youtube.com/watch?v=gV1fAvgHHhc) |

## Repository Contents

```text
.
├── docs/
│   └── assets/       # Project photography and demonstration thumbnails
├── ATTRIBUTION.md    # Re-use guidance and citation format
├── CITATION.cff      # Machine-readable academic citation
├── LICENSE           # BSD 3-Clause license
└── README.md         # Project documentation
```
