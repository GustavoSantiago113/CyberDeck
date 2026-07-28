<div align="center">

# Solar Punk CyberDeck

A CyberDeck inspired on the Solar Punk theme

</div>

---

- [Solar Punk CyberDeck](#solar-punk-cyberdeck)
  - [Mission Definition](#mission-definition)
    - [Purpose](#purpose)
    - [Project Goals](#project-goals)
    - [Unique Characteristics](#unique-characteristics)
  - [Requirements Engineering](#requirements-engineering)
  - [System Architecture](#system-architecture)
    - [Electronics](#electronics)
    - [Architecture](#architecture)

---

## Mission Definition

### Purpose

The purpose of this is to have a distinct portable computer to take to the field and perform on-site prototyping on electronics and tests on field data, at the field.

### Project Goals

- Battery Life goal: 4 hours
- Target weight: 2kg
- Target budget: US$ 300

### Unique Characteristics

- Solar panels to help recharge
- Wood and leather parts
- Free GPIOs for electronics/mechatronics prototyping
- Usage for field quick data analysis / imagery algorithm testing
- Battery display
- Leaf-inspired vent geometry

---

## Requirements Engineering

| Section | Part | Item/Requirement |
| ------- | ---- | ---------------- |
| Hardware | Screen size | 7 " |
| Hardware | Keyboard size | Max of 12 " |
| Hardware | Battery capacity | 10,000 mAh |
| Hardware | Storage | HD of 150GB |
| Hardware | CPU/GPU? | CPU |
| Hardware | Connectivity | Bluetooth, WiFi, Ethernet, USBs, Anthena for Wi-Fi longer range |
| Software | Operating System | Linux, obviously |
| Software | Programming environment | Mostly Python, but if needed, C-family for speedness |
| Software | AI tools | Claude, but if no connection, God help me |
| Software | Robotics tools | GPIO exposed |
| Software | CAD software | FreeCAD |
| Performance | Battery target | 4 hours |
| Performance | Temperature limits | 60 degrees |
| Performance | Boot time | Up to 2 minutes |
| Performance | Weight | 2kg |
| Performance | Noise level | Low to Medium |

---

## System Architecture

### Electronics

* RaspberryPi 5
* 7" Touchscreen display
* Ultra Thin USB Mini Wired Keyboard (11.2")
* 10,000 mAh Power Bank with pass-through charging
* Home-made fan with motor and leaf-inspired 3D printed parts
* USB Wi‑Fi adapter with removable antenna
* 5V Solar Panel (12W) + Solar USB Charger Controller + Outlet charger
* USB Hub connecting parts
* 128GB External HD + 32GB SD Card

### Architecture

<center> 

**System Block Diagram**

<img src="docs/System Block Diagram.png">

</center>


<center> 

**Mechanical Block Diagram**

<img src="docs/Mechanical Block Diagram.png">

</center>