# Solarpunk CyberDeck Build Protocol

---

## Solarpunk Feature Ideas

Instead of decorative LEDs, make the machine visibly sustainable and repairable:

* 🌱 **Integrated solar lid:** A slim solar panel mounted on the lid that trickle-charges the battery while outdoors.
* 🌿 **Living ventilation:** Leaf-inspired vent geometry that directs airflow efficiently and doubles as a visual motif.
* 🔧 **Repair-first construction:** Every major component is accessible with standard hex screws; no glue, and modular printed panels can be replaced individually.
* 🪵 **Natural material accents:** Bamboo or walnut side grips, cork wrist rests, or leather carrying straps paired with printed structural parts.
* 🔋 **Energy awareness:** An e-ink status display showing battery level, solar input, and power consumption even when the main system is off.
* 📦 **Modular expansion:** Magnetic or rail-mounted side modules (e.g., SDR, sensor suite, extra battery, or storage) that can be swapped without opening the main enclosure.

---

## Phase 0 — Define the Mission

**Goal:** Determine what the cyberdeck is supposed to do.

### Write the Project Brief

Answer:

* What problems should it solve?
* Where will it be used?
* Weight limit?
* Battery life target?
* Budget?
* Future upgrades?

Example:

> "Portable Linux workstation for programming, robotics, CAD viewing, field data collection, and AI inference with 8+ hours of battery."

---

## Phase 1 — Requirements

### Functional Requirements

Decide whether you need:

* Programming
* CAD
* Electronics work
* SDR
* GPS
* ROS Robotics
* AI
* Networking
* Ham radio
* Drone control
* Photography backup
* Server administration

### Performance Requirements

Example

* Boots under 30 seconds
* 8-hour battery
* Fan noise below 30 dB
* Fits inside a backpack
* Waterproof to light rain

---

## Phase 2 — Hardware Architecture

Now design the whole computer before buying anything.

### Main Computer

Choose one:

* Raspberry Pi 5
* Jetson Orin Nano (excellent since you already have one)
* Mini PC
* Framework motherboard
* LattePanda


### Display

Choose

* Size
* Resolution
* Brightness
* Touch or non-touch

### Input

Choose

* Mechanical keyboard
* Split keyboard
* Trackball
* Touchpad
* TrackPoint
* Rotary encoder

### Power

Design

Battery

↓

Protection

↓

Charging

↓

Voltage regulation

↓

Computer

↓

Display

↓

USB devices

### Expansion

Leave room for

* SSD
* SDR
* GPS
* LoRa
* USB hub
* Ethernet
* GPIO access

---

## Phase 3 — Solarpunk Design Language

Instead of cyberpunk blacks and neon...

Think

### Materials

* Warm white
* Sand
* Olive green
* Copper
* Bamboo accents
* Walnut inserts
* Brass screws
* Linen straps
* Cork grips

### Shapes

Avoid sharp military angles.

Use

* Rounded corners
* Organic curves
* Visible structural ribs
* Honeycomb vents
* Leaf-inspired patterns

### Functional aesthetic

Every detail should have a purpose.

Examples

* Solar panel doubles as lid.
* Cooling fins become decorative ribs.
* Cable channels become visible "vines."
* Battery indicator resembles a seed gauge.

---

## Phase 4 — CAD

This phase is huge.

### Learn constraints

Measure every component.

Never model from internet dimensions.

Use calipers.

### Model

1. Motherboard
2. Display
3. Keyboard
4. Batteries
5. Speakers
6. USB ports
7. Hinges
8. Screws


**Build around the components, not the other way around.**


### Assemble virtually

Check

* Cable routing
* Cooling
* Clearances
* Maintenance

---

## Phase 5 — Thermal Design

Map heat sources.

CPU

↓

Heat sink

↓

Air path

↓

Fan

↓

Exhaust

Never trap hot air.

---

## Phase 6 — Power System

Design

Solar Panel

↓

MPPT Charger

↓

Battery

↓

Battery Management System

↓

USB-C PD

↓

Computer

↓

Accessories

Questions:

* Internal battery?
* Swappable batteries?
* External solar charging?
* USB-C charging?

---

## Phase 7 — Electronics

Design wiring.

Avoid spaghetti cables.

Use

* JST connectors
* Ferrules
* Braided sleeves
* Heat shrink
* Wire labels

Create a wiring diagram before assembling.

---

## Phase 8 — Manufacturing

### Print prototypes

Prototype 0

Only verify dimensions.

Prototype 1

Verify fit.

Prototype 2

Verify ergonomics.

Final

High-quality settings.

### Printing checklist

- Orientation

- Supports

- Strength

- Layer height

- Threaded inserts

- Heat-set inserts

---

## Phase 9 — Assembly

Order

1. Heat-set inserts
2. Hinges
3. Display
4. Keyboard
5. Wiring
6. Cooling
7. Motherboard
8. Batteries
9. Final shell

---

## Phase 10 — Software

Install

* Linux
* Drivers
* Terminal customization
* SSH
* Docker
* Git
* VS Code
* ROS
* Python
* Monitoring software

Configure

* Auto-backup
* Battery monitoring
* Temperature monitoring
* Fan control

---

## Phase 11 — Testing

### Mechanical

- Opens smoothly

- Doesn't wobble

- Comfortable typing

- Backpack safe


### Electrical

- Battery

- Charging

- USB

- Display

- Wi-Fi

- Bluetooth

- GPIO

### Thermal

Run stress tests.

Monitor

* CPU
* GPU
* Battery


### Field Test

Take it somewhere. Actually use it. Find what annoys you. Iterate.

---

## Phase 12 — Refinement

Improve

* Weight
* Cable routing
* Ventilation
* Grip
* Software
* Boot time

Repeat until satisfied.