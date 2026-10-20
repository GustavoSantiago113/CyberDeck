# CyberDeck Build Protocol — Jetson Orin Nano Field Deck

A portable deck for the field and the greenhouse, used for **raw data analysis, IoT prototyping and coding**, with a **small coding-agent LLM running offline**. It does not collect data itself: datasets come in from the collection setup, and IoT devices are built and debugged on it.

Schedule: [timeline.md](timeline.md) · Legend: ✅ = already on hand / already done
Project Goals: [goals.md](goals.md)
Design Notes: [design_notes.md](design_notes.md)
Bill of Materials: [BOM.md](BOM.md)
Deliverables write-ups: [deliverables.md](deliverables.md)

---

# 🎯 Phase 0 — Mission Definition

**Week 1** · **Goal:** a clear purpose and measurable project goals.

* - [X] Define the purpose: raw field analysis, on-site IoT prototyping, offline coding
* - [X] Set the project goals
* - [ ] Read the power bank label: 5V output current per port, combined output limit, input rating
* - [ ] Inventory the parts on hand

### Deliverables

* Purpose, project goals, and table of the parts on hand

---

# 📐 Phase 1 — Requirements Engineering

**Week 1** · **Goal:** measurable requirements, frozen before ordering.

### Hardware

* - [ ] Screen size — 7" HDMI, USB touch, ≥ 400 nits
* - [ ] Keyboard size — 11.2" ✅
* - [ ] Battery capacity — 10,000 mAh with pass-through ✅
* - [ ] Storage — 512GB NVMe (OS + models) + 256GB external HD (datasets) + 32GB SD (recovery)
* - [ ] CPU/GPU — Jetson Orin Nano 8GB (CUDA)
* - [ ] Connectivity — USB Wi-Fi adapter with external antenna, internal Bluetooth, USB-A

### Software

* - [ ] Operating System — JetPack 6.x (Ubuntu 22.04)
* - [ ] Programming environment — Python first, C/C++ / CUDA when needed
* - [ ] AI tools — local coding agent offline (ready-made agent-tuned model + Aider/Continue), Claude Code when online
* - [ ] IoT tools — 40-pin GPIO (`Jetson.GPIO`), PlatformIO on VSCode for ESP32/Arduino, MQTT test broker

### Performance

* - [ ] Battery target — ≥ 2 h heavy, ~3 h light, unlimited when plugged in
* - [ ] Temperature limits — no throttling in 7 W mode at 35 °C ambient; battery and outer case < 45 °C
* - [ ] Boot time — up to 2 minutes
* - [ ] Weight — ≤ 3 kg with charger and kit
* - [ ] Noise level — low to medium
* - [ ] LLM — 3B–4B Q4 coding model with tool calling, 16k context, ≤ 4 GB RAM including context, measured tok/s

### Deliverables

* Requirement Specification

---

# 🧩 Phase 2 — System Architecture

**Weeks 1–2** · **Goal:** a complete system design and parts ordered in week 1.

### Electronics

* - [ ] Motherboard — Jetson Orin Nano 8GB Super Dev Kit
* - [ ] Display — 7" HDMI + USB touch, DP→HDMI adapter
* - [x] Keyboard — Ultra Thin USB Mini Wired Keyboard (11.2") ✅
* - [x] Battery — 10,000 mAh power bank with pass-through ✅
* - [ ] Power — 5V → 12V boost (≥ 24 W), switch, fuse, bulk cap, USB-C panel input
* - [ ] Cooling — Jetson stock heatsink + fan
* - [x] Wi-Fi — USB adapter with external antenna ✅ (driver check in Phase 3)
* - [x] Charging — outlet charger ✅
* - [ ] Memory — 512GB NVMe + 256GB external HD ✅ + 32GB SD ✅
* - [ ] IoT kit — 2× ESP32-S3, half breadboard, jumpers, sensors

### Architecture

* - [ ] System Block Diagram
* - [ ] Mechanical Block Diagram (compute in base, storage bay under keyboard)
* - [ ] Power wiring diagram

### Purchasing

* - [ ] Parts spreadsheet / BOM
* - [ ] **Order components by 23 Oct**

### Deliverables

* System Architecture Diagram
* Bill of Materials

---

# 🔌 Phase 3 — Bench Bring-up (Go / No-Go)

**Week 3** · **Goal:** prove power, display and Wi-Fi on the bench before CAD.

* - [ ] Flash JetPack 6.x to NVMe; keep the SD as a recovery image
* - [ ] Set the boost to 12V, then power the Jetson from the bank through the switch and fuse
* - [ ] Lock 7 W mode (`nvpmodel`); stress test for 30 min with all peripherals, no brownout
* - [ ] Measure the draw at the bank with the inline meter (idle / analysis / LLM)
* - [ ] Pass-through: plug in the charger while running, check for no reboot
* - [ ] Display through DP→HDMI, touch working
* - [ ] USB Wi-Fi adapter: identify the chipset (`lsusb`), install the ARM64 driver, prefer it over the internal Wi-Fi
* - [ ] Keyboard, hub, HD, Bluetooth working
* - [ ] **Decision:** go, or replace the boost / bank / display

### Deliverables

* Working bench system + measured power numbers

---

# 🧠 Phase 4 — Local Coding LLM

**Weeks 3–6 (parallel)** · **Goal:** a ready-made coding-agent model working offline as an agent, with no training.

## Weeks 3–4 — Runtime & Model

* - [ ] Install Ollama, or build `llama.cpp` with CUDA (`llama-server --jinja` for tool calls)
* - [ ] Download 2–3 agent-tuned coding models (3B–4B, Q4 GGUF, tool calling); store them on the NVMe
* - [ ] Benchmark each in 7 W mode at 16k context: prompt processing + generation tok/s, RAM, watts
* - [ ] Tune memory: KV cache q8_0, context size, lightweight desktop (XFCE) / zram

## Weeks 5–6 — Agent Setup

* - [ ] Aider in the terminal, pointed at the local server
* - [ ] VS Code + Continue (agent mode) or Cline; check that tool calls work reliably
* - [ ] Write 10 test tasks from your real work (sensor script, ESP32 MQTT client, fix a notebook bug, explain a traceback)
* - [ ] Run the tasks on each model × front end; pick the best combination
* - [ ] Project rules file (coding conventions, Jetson/ESP32 pinouts, your libraries)
* - [ ] Local docs folder of datasheets and notes for the agent to search
* - [ ] LLM server as a systemd service, started on demand (frees RAM when not used)
* - [ ] One-command switch: local agent offline ↔ Claude Code online

### Deliverables

* Working offline coding agent + benchmark and task-success table

---

# ✏️ Phase 5 — Industrial Design & CAD

**Weeks 2 and 4** · **Goal:** a complete CAD assembly with every part fitted.

## Week 2 — Component Modeling

* - [x] Shell, hinges, latches, handle ✅
* - [ ] Jetson dev kit model (start from NVIDIA's published 3D model before it arrives)
* - [ ] Measure display + driver board, boost, power bank, charger, HD, hub
* - [ ] Measure the depth under the keyboard (decides where the charger goes)

## Week 4 — Layout & Parts

* - [ ] Cover Bottom: Jetson + bank layout, thermal wall, intake grille, cable routing
* - [ ] Port bezel: USB-C power in, power switch, Ethernet, USB-A
* - [ ] I/O strip: GPIO breakout, Qwiic/I²C, 2× USB-A, hub + HD mount underneath
* - [ ] Keyboard lift-up tray (hinge + magnets)
* - [ ] Under-keyboard bay: charger cradle + cable groove + removable IoT kit tray
* - [ ] Cover Top: display bezel, USB Wi-Fi slot, plain finish
* - [ ] Hinge cable path: FPC HDMI + USB
* - [ ] Printed feet (~8 mm)
* - [ ] Lid balance check

### Deliverables

* Complete CAD assembly

---

# 🌡 Phase 6 — Thermal Engineering

**Weeks 3–4** · **Goal:** no throttling at 7 W, cool battery.

* - [ ] Locate heat sources: Jetson, boost converter, power bank, display
* - [ ] Measure SoC temperature (`tegrastats`, `jtop`) in an open-air bench setup
* - [ ] Design the intake grille + mesh, point the exhaust at the side vents
* - [ ] Place the boost in the airflow
* - [ ] Fan curve

### Deliverables

* Thermal layout + measurements

---

# 🔋 Phase 7 — Power System

**Weeks 3–4** · **Goal:** one plug in, one switch, measured runtime.

* - [x] Cells + BMS — integrated in the power bank ✅
* - [ ] USB-C panel input → bank input (pass-through)
* - [ ] Bank 5V → switch → fuse → boost 12V → bulk cap → barrel jack
* - [ ] Battery monitoring — bank display visible through a window + inline meter
* - [ ] Runtime measured per use case

### Deliverables

* Wiring diagram + measured power budget

---

# 🖨 Phase 8 — Manufacturing

**Weeks 5–6** · **Goal:** all new parts printed (PETG near heat).

## Week 5 — Prototype

* - [ ] Test-print the port bezel, Jetson bracket, charger cradle and keyboard hinge
* - [ ] Verify tolerances, adjust CAD

## Week 6 — Final Prints

* - [x] Case Top, Case Bottom, Handle, Latches, Hinge Pin ✅
* - [ ] Cut the side-wall window in the Case Bottom
* - [ ] Cover Bottom (PETG), Cover Top
* - [ ] Port bezel, I/O strip, Jetson bracket, keyboard tray, IoT kit tray, feet

### Deliverables

* Finished printed parts + STLs in `3D Prints/`

---

# 🔧 Phase 9 — Assembly

**Week 7** · **Goal:** a fully assembled, self-contained deck.

Mechanical

* - [x] Inserts, enclosure, hinges ✅
* - [ ] Port bezel, I/O strip, keyboard tray, feet

Electronics

* - [ ] Jetson + NVMe
* - [ ] Power chain: panel input, bank, switch, fuse, boost, capacitor
* - [ ] Display + driver; FPC HDMI + USB through the hinge
* - [ ] USB Wi-Fi adapter in the lid slot
* - [ ] Hub + HD under the I/O strip; GPIO ribbon to the breakout
* - [ ] Charger cradle + IoT kit tray packed; silica gel

### Deliverables

* Fully assembled CyberDeck

---

# 💻 Phase 10 — Software

**Weeks 3 and 7** · **Goal:** a ready-to-use analysis and prototyping system.

Operating System

* - [ ] JetPack 6.x on NVMe, SSH, Docker (NVIDIA runtime), VS Code, Claude Code
* - [ ] Terminal config, 7 W mode locked at boot, `jtop`

Analysis

* - [ ] JupyterLab, pandas/polars, scikit-learn, matplotlib, OpenCV, CUDA PyTorch
* - [ ] Import workflow: HD / SD / network → analysis folder
* - [ ] Notebook templates for your usual raw analyses

IoT Prototyping

* - [ ] PlatformIO / Arduino CLI / ESP-IDF; flash and serial monitor over USB
* - [ ] `Jetson.GPIO` + `smbus2` sensor test scripts
* - [ ] Local Mosquitto broker for testing MQTT code
* - [ ] Backup: rsync / Syncthing of code and notebooks

### Deliverables

* Fully configured system

---

# 🌍 Phase 11 — Testing

**Week 8 (Mon–Thu)** · **Goal:** prove every project goal with numbers.

### Mechanical

* - [ ] Port, I/O strip and storage bay access
* - [ ] Hinge with cables (100 open/close cycles)
* - [ ] Lid balance, keyboard tray stability, nothing rattles when shaken
* - [ ] Total weight with charger + kit ≤ 3 kg

### Electrical

* - [ ] Runtime: light, analysis + LLM, sustained LLM
* - [ ] Pass-through: runs indefinitely on the single plug, no reboot on plug/unplug
* - [ ] USB: all ports with the full load (HD + Wi-Fi + display + ESP32)

### Thermal

* - [ ] CPU + GPU stress for 30 min in 7 W mode
* - [ ] Sustained LLM generation for 15 min
* - [ ] Greenhouse ambient test (throttling, battery and case temperature)

### Field

* - [ ] Raw analysis of a real dataset on site
* - [ ] Debug and re-flash an IoT device on site using the carried kit
* - [ ] Offline coding session with the local agent only (complete 3 real tasks)
* - [ ] Backpack transport, humidity and dust exposure

### Deliverables

* Test report + issue list

---

# 🔁 Phase 12 — Refinement & Documentation

**Week 8 (Fri–Sat)** · **Goal:** fix what testing found and document the build.

### Improvements

* - [ ] Fix design issues
* - [ ] Cable management
* - [ ] Cooling and fan curve
* - [ ] Weight
* - [ ] Software configuration

### Documentation

* - [ ] README (gallery, specs, BOM, block diagrams)
* - [ ] FreeCAD source files + STEP + STL
* - [ ] Wiring diagram
* - [ ] Build log with photos
* - [ ] User manual (power switch, charging, LLM, IoT kit)
* - [ ] Maintenance guide (intake mesh, silica gel, re-flash from SD)

### Deliverables

* Documented CyberDeck

---

# 📄 Phase 13 — Hardware Paper

**Weeks 5–8 (parallel, ready 13 Dec)** · **Goal:** a submission-ready open-hardware paper.

Structure follows the open-hardware journal format (e.g., *HardwareX*; alternative: *Journal of Open Hardware*). Check the chosen journal's current author guidelines before drafting. Build each paper section from the matching write-ups in [deliverables.md](deliverables.md) (each one is tagged 📄 with its section).

### Week 5 — Plan

* - [ ] Choose the target venue and download its template
* - [ ] Outline + figure list (block diagrams, CAD renders, power chain, layout, photos)
* - [ ] Collect references (other cyberdecks, edge-AI devices, field computers for agriculture)

### Weeks 6–7 — Draft (no test data needed)

* - [ ] Specifications table (hardware name, subject area, cost, license, repository)
* - [ ] Hardware in context — why a field deck for greenhouse analysis and IoT prototyping
* - [ ] Hardware description — architecture, power chain, layout, carry system, offline LLM
* - [ ] Design files summary — every CAD/STL file with license and location
* - [ ] Bill of materials — part, quantity, cost, source
* - [ ] Build instructions — step by step with photos, safety notes (lithium, boost wiring)
* - [ ] Operation instructions — power, charging, modes, LLM, IoT workflow

### Week 8 — Validation & Final

* - [ ] Validation and characterization: runtime, power draw, thermals, LLM tok/s, agent task success rate, weight, boot time — measured against the Project Goals
* - [ ] Limitations and future work (e.g., PD trigger for 15 W mode, larger battery)
* - [ ] Abstract, keywords, figures and tables final
* - [ ] Archive the design files with a DOI (Zenodo/OSF) under the repo's MIT license (and an open-hardware license for CAD, if the venue requires it)
* - [ ] Proofread; author contributions, acknowledgements, conflict of interest statement

### Deliverables

* ✅ Submission-ready hardware paper + archived design files
