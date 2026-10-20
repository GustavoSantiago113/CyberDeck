# 📦 Deliverables

**How to use it**
- Write as soon as a deliverable is done, while you still remember the details.
- Write in plain language: short sentences, one idea each. Say **what** you did, **why**, and **what happened**.
- Always give numbers with units (W, h, °C, g, tok/s, US$).
- Mark anything still missing with `[TODO]`.
- Save photos and screenshots in `Images/` and link them here.
- Each section names the paper section it feeds (📄).

**Status:** ⬜ not started · 🟨 in progress · ✅ done

---

## Phase 0 — Purpose and Project Goals

**Status:** 🟨 · 📄 *Hardware in context*, *Specifications table*

**What the deck is.**
The CyberDeck is a small portable computer in a 3D-printed case. I will take it to the field and to the greenhouse to look at data collected over there, build, debug and fix IoT devices, and write code. It runs an AI coding assistant on the device itself and Claude Code so it can work without internet.

**What it is not.**
It does not collect data. The sensors, loggers, and cameras in the greenhouse and field do that. The deck reads and analyze their data afterwards.

**Why I built it.**
A normal laptop is not made for the greenhouse and mainly not the field: it is fragile, more expensive it has no pins for wiring sensors and actuators, and its AI tools may need internet. I wanted one box that has a screen, a keyboard, a battery, pins for electronics, a kit of parts, and an AI helper that works offline. Some real situations that I can use this:

- Check the readings of a homemade weather station, and if something is wrong, debug in the local.
- Get images from the smartphones that are being used to collect imagery data in the field, and check the results of our machine learning models on them. If the images would need to be re-taken, we can already do it in the field and re-check.
- In-field testing of sensors and actuators without having to take my desktop computer (impossible) or company's laptop there.

**Project goals** (from [goals.md](goals.md))

| Goal | Target |
| ---- | ------ | 
| Battery life | ≥ 2 h heavy use, ~3 h light use, unlimited plugged in | 
| Power input | One plug charges and runs the deck | 
| Weight | ≤ 3 kg with charger and kit | 
| Local AI | 3B–4B coding-agent model working offline | 
| Carry | Charger + IoT kit inside the case | 
| Schedule | Done by 13 Dec 2026 | 
| Budget | ~US$ 500 | 

**Power Bank reading:** `[TODO: Add voltage and current of the power bank]`
**Parts on Hand:** `[TODO: table of the parts on hand]`

---

## Phase 1 — Requirement Specification

**Status:** ⬜ · 📄 *Specifications table*, *Hardware description*

**In plain words**
Before buying anything, I wrote down what the deck must do, as numbers I can test later.

| Area | Requirement | Why |
| ---- | ----------- | --- |
| Screen | 7", touch, bright enough for a greenhouse (≥ 400 nits) | Fits the case; readable in daylight |
| Keyboard | 11.2" | Fits the case; full-size keys |
| Battery | 10,000 mAh with pass-through | Already owned; can run and charge at the same time |
| Computer | Jetson Orin Nano 8GB | Has a GPU, so it can run an AI model and fast analysis |
| Storage | 512GB NVMe + 256GB external HD + 32GB SD | Fast drive for the system, removable drive for datasets, SD for recovery |
| Wi-Fi | USB adapter with external antenna | Better range in the greenhouse |
| Temperature | No slowdown at 35 °C room; battery and case < 45 °C | Greenhouses get hot |
| Weight | ≤ 3 kg | Carried by one hand |
| Boot time | ≤ 2 min | |
| AI | 3B–4B coding model, 16k context, ≤ 4 GB memory | Fits in 8 GB with everything else |

**Evidence:** link to the requirements in [todos.md](todos.md)

---

## Phase 2 — System Architecture and Bill of Materials

**Status:** ⬜ · 📄 *Hardware description*, *Bill of materials*

**In plain words**
The power bank feeds everything. Its 5 V output goes through a switch and a fuse to a small board that raises it to 12 V, which is what the Jetson needs. The Jetson then powers the screen, keyboard, Wi-Fi adapter and a USB hub. One USB-C plug on the side of the case charges the power bank, and the deck keeps running while it charges.

**Figures to include**
- [ ] System block diagram `[TODO: export from Diagrams.pptx]`
- [ ] Mechanical block diagram
- [ ] Power wiring diagram

**Key design choices** (one line each: the choice → why)
- Computer in the base, not the lid → heat stays away from the screen, and the lid doesn't tip back.
- Battery and computer separated by a wall → keeps the battery cool.
- Power from 5 V with a boost converter → simple, works with the power bank I have. Limit: the Jetson must run in its 7 W mode.
- Charger and IoT kit stored under the keyboard → weight stays low, and the case stays balanced.

**Cost:** total `US$ [TODO]` (from [BOM.md](BOM.md)) · parts reused from what I owned: `US$ 85.31`

---

## Phase 3 — Bench Bring-up

**Status:** ⬜ · 📄 *Validation and characterization*

**In plain words**
Before designing the case, I connected everything on the table to check that it works.

| Check | Result | Notes |
| ----- | ------ | ----- |
| Jetson starts from the power bank through the boost | `[TODO]` ✅ / ❌ | |
| 30-minute stress test without shutting down | `[TODO]` | |
| Plugging in the charger while running doesn't restart it | `[TODO]` | |
| Screen shows an image; touch works | `[TODO]` | |
| USB Wi-Fi adapter works (chipset: `[TODO]`) | `[TODO]` | |
| Power draw at the bank: idle / analysis / AI | `[TODO] W / [TODO] W / [TODO] W` | |

**Decision:** `[TODO: go, or what was replaced and why]`

**Evidence:** `[TODO: photo of the bench setup, screenshot of tegrastats]`

---

## Phase 4 — Offline Coding Agent

**Status:** ⬜ · 📄 *Hardware description*, *Validation and characterization*

**In plain words**
The deck runs a small AI model already trained to write code and use tools. An agent program (Aider or Continue) lets it read and edit files and run commands. No internet is needed.

| Model | Size | Memory used | Speed (tok/s) | Tasks passed (of 10) |
| ----- | ---- | ----------- | ------------- | -------------------- |
| `[TODO]` | | | | |
| `[TODO]` | | | | |

**Chosen setup:** `[TODO: model + agent tool, and why]`

**What it's good at / not good at:** `[TODO: 2–3 honest sentences]`

---

## Phase 5 — CAD Assembly

**Status:** ⬜ · 📄 *Design files summary*, *Hardware description*

**In plain words**
I kept the shell, hinges, latches and handle from my existing case design and redesigned the inside to fit the new parts.

| Part | New or kept | Material | File |
| ---- | ----------- | -------- | ---- |
| Case Top / Case Bottom | Kept (side window cut) | PLA | `3D Prints/` |
| Handle, Latches, Hinge Pin | Kept | PLA | `3D Prints/` |
| Cover Top (screen frame) | New | `[TODO]` | `[TODO]` |
| Cover Bottom (inner deck) | New | PETG | `[TODO]` |
| Port panel | New | PETG | `[TODO]` |
| I/O strip | New | `[TODO]` | `[TODO]` |
| Keyboard tray | New | `[TODO]` | `[TODO]` |
| IoT kit tray | New | `[TODO]` | `[TODO]` |

**Evidence:** `[TODO: CAD renders — open, closed, exploded, storage bay]`

---

## Phase 6 — Thermal Layout

**Status:** ⬜ · 📄 *Validation and characterization*

**In plain words**
Cool air comes in through a meshed grille under the base and leaves through the side vents. The battery sits behind a wall, away from the hot air.

| Test | Result |
| ---- | ------ |
| Chip temperature, 30 min stress at 7 W | `[TODO] °C` |
| Slowed down (throttled)? | `[TODO]` |
| Battery temperature | `[TODO] °C` |
| Outside of case, hottest spot | `[TODO] °C` |
| Room temperature during the test | `[TODO] °C` |

---

## Phase 7 — Power System

**Status:** ⬜ · 📄 *Hardware description*, *Validation and characterization*

**In plain words**
`[TODO: describe the chain in your own words — plug → power bank → switch → fuse → boost → Jetson]`

| Use | Power at bank | Measured runtime | Target |
| --- | ------------- | ---------------- | ------ |
| Light coding / IoT prototyping | `[TODO] W` | `[TODO] h` | ~3 h |
| Analysis + AI questions | `[TODO] W` | `[TODO] h` | ≥ 2 h |
| Non-stop AI generation | `[TODO] W` | `[TODO] h` | ≥ 2 h |
| Plugged in | — | `[TODO]` | Unlimited |

**Safety notes for builders:** `[TODO: fuse, polarity, set the boost to 12 V before connecting, lithium battery care]`

---

## Phase 8 — Printed Parts

**Status:** ⬜ · 📄 *Build instructions*

| Part | Material | Print time | Filament (g) | Settings (layer, infill) | Problems / fixes |
| ---- | -------- | ---------- | ------------ | ------------------------ | ---------------- |
| `[TODO]` | | | | | |

---

## Phase 9 — Assembly

**Status:** ⬜ · 📄 *Build instructions*

Write each step as one action, with a photo:

1. `[TODO]`
2. `[TODO]`

**Tools needed:** `[TODO]` · **Time to assemble:** `[TODO] h`

---

## Phase 10 — Software Setup

**Status:** ⬜ · 📄 *Operation instructions*

| What | Tool / version |
| ---- | -------------- |
| Operating system | JetPack `[TODO]` |
| Analysis | `[TODO]` |
| IoT prototyping | `[TODO]` |
| AI agent | `[TODO]` |

**Daily use, step by step:** `[TODO: switch on → open project → plug in sensor → analyse → switch off]`

---

## Phase 11 — Test Report

**Status:** ⬜ · 📄 *Validation and characterization*

| Test | Target | Result | Pass? |
| ---- | ------ | ------ | ----- |
| Battery, heavy use | ≥ 2 h | `[TODO]` | |
| Battery, light use | ~3 h | `[TODO]` | |
| Runs on the single plug | Unlimited, no restarts | `[TODO]` | |
| Weight with charger + kit | ≤ 3 kg | `[TODO]` | |
| Boot time | ≤ 2 min | `[TODO]` | |
| Chip temperature, greenhouse | No slowdown | `[TODO]` | |
| Hinge, 100 open/close cycles | No damage | `[TODO]` | |
| Offline coding: 3 real tasks | 3 done | `[TODO]` | |
| Fix an IoT device on site with the kit | Done | `[TODO]` | |

**Issues found:** `[TODO: list → what you changed]`

---

## Phase 12 — Final Documentation

**Status:** ⬜ · 📄 *Design files summary*, *Operation instructions*

- [ ] README updated
- [ ] CAD source + STEP + STL files in the repo
- [ ] Wiring diagram
- [ ] Build log with photos
- [ ] User manual
- [ ] Maintenance guide

**Limitations and future work** (write these down as you find them):
- Runs only in the Jetson's 7 W mode because of the 5 V power path. A 12 V USB-C PD trigger would allow 15 W.
- `[TODO]`
