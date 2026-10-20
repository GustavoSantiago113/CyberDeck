# 🛠 Design Notes

## Hardware

**On hand:** printed shell (Case Top/Bottom, Covers, Handle, Latches, Hinge Pin), ultra-thin USB keyboard (11.2"), 10,000 mAh power bank with pass-through, outlet charger, USB Wi-Fi adapter with external antenna, 7-port USB hub, 256GB external HD, 32GB SD card, filament.

**To buy:** Jetson Orin Nano 8GB Super Dev Kit, 512GB NVMe, 7" HDMI display with USB touch, DP→HDMI adapter, slim FPC HDMI cable (through the hinge), 5V→12V boost converter, panel-mount USB-C extension, latching power switch + inline fuse, bulk capacitor, PETG filament, inline USB power meter, IoT kit parts.

**Jetson facts that drive the design**
- Power goes in through the **DC barrel jack (5.5×2.5 mm, ~9–19V)**. The Jetson's USB-C port is data only.
- Video comes out of **DisplayPort only**, so a 7" HDMI panel needs a DP→HDMI adapter. Small 1024×600 panels can fail to show an image. Pick a standard resolution (1280×720/800 or 1920×1080) and a seller with returns.
- **No ADC; GPIO is 3.3V.** Use an ESP32/RP2040 for analog and 5V sensors.
- **Only 4 USB-A ports:** keyboard, Wi-Fi adapter, display touch and the hub. The hub feeds the HD and the I/O strip.

## Power System — one plug in, one switch

```
Outlet charger ─► [USB-C panel input on case] ─► Power bank (pass-through)
                                                     │ 5V USB
                                                     ▼
                                    [latching switch] ─ [fuse 4A]
                                                     ▼
                                Boost 5V → 12V (rated ≥ 24 W) ─ bulk cap 2200 µF/25V
                                                     ▼
                                     5.5×2.5 barrel ─► Jetson Orin Nano
                                                     ▼ USB 5V
                           keyboard · Wi-Fi adapter · display · hub (HD, I/O strip)
```

- **The 5V path is the limit.** One USB port at 5V/3A gives ~15 W in and ~13.5 W after the boost, for *everything* (Jetson, display, HD, peripherals). So the Jetson runs locked in **7 W mode**; 15 W and 25 W modes won't fit. If you later need more power, swap the boost for a 12V USB-C PD trigger cable. The rest of the design stays the same.
- **Boost choice:** rated ≥ 24 W so it runs cool at ~13 W. Most "USB to 12V" cables are only 0.8–1 A, which is too weak. Set it to 12V before connecting the Jetson.
- **Feeding the boost from the bank's USB-C port:** use a USB-C breakout with 5.1 kΩ CC resistors, or the bank won't turn on its 5V. Its USB-A port works without them but is often limited to 2.4 A.
- **Bulk capacitor** on the boost output so the Jetson rides through the short output drop some banks have when the charger is plugged in.
- **Single input:** a panel-mount USB-C on the port bezel, wired to the bank's input. Use a charger rated above the bank's max input (e.g., ≥ 20 W) so pass-through covers the ~13 W load.
- **One latching switch** between bank and boost. The Jetson powers on as soon as it gets power, and the switch also stops the boost from draining the bank while the deck is off.
- Keep the boost in the airflow, not against the bank (it dissipates ~1.5 W).

**Battery budget** (10,000 mAh × 3.7V ≈ 37 Wh → plan ~28 Wh after bank and boost losses; estimates, to be measured in Phase 3)

| Use | Draw at bank | Runtime |
| --- | ------------ | ------- |
| Light coding / IoT prototyping | ~9 W | ~3 h |
| Raw analysis + LLM queries | ~11 W | ~2.5 h |
| Sustained LLM generation | ~13–14 W | ~2 h |
| Plugged in (pass-through) | — | Unlimited |

The external HD is the largest optional load. If it's a spinning drive, it also has a start-up current spike, so plug it in only when moving datasets. Keep it padded, and don't move the deck while it's spinning.

## Layout

**Base** (top view, hinge at the back, handle on the left):

```
                              HINGE  (FPC HDMI + USB pass here)
 ┌──────────────────────────────────────────────────────────────────┐
 │  ┌──────────────────────┐ ┃ ┌──────────────────────────┐         │
 │  │ POWER BANK           │ ┃ │ JETSON ORIN NANO         │  ≋≋     │ ← exhaust → existing side vents
H│  │ (fixed, pass-through)│ ┃ │ fan up · NVMe underneath │  ≋≋     │
A│  │ battery display ▣    │ ┃ │ boost converter in flow  │  ▤      │ ← PORT BEZEL: USB-C power in ·
N│  └──────────────────────┘ ┃ └──────────────────────────┘         │   power switch · Ethernet · USB-A
D│                 thermal wall / air gap    ▲ bottom intake + mesh │
L│ ═══ I/O STRIP: 40-pin GPIO breakout · Qwiic/I²C · 2× USB-A ═══    │ ← hub + HD underneath
E│  ┌────────────────────────────────────────────────────────────┐  │
 │  │  KEYBOARD — lifts up on a hinge / magnets                  │  │
 │  │  ┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄  │  │
 │  │  UNDER-KEYBOARD BAY: charger + cable · IoT kit tray        │  │
 │  └────────────────────────────────────────────────────────────┘  │
 └──────────────────────────────────────────────────────────────────┘
                                LATCHES (front)
```

- **Compute in the base, not the lid.** The heat stays away from the display, the lid doesn't get top-heavy, and only the display cable and USB cross the hinge.
- **Battery and Jetson on opposite sides of a wall.** Keep the cells below ~45 °C, and never point exhaust at the bank.
- **Bottom intake → side exhaust** through the existing vent slots. Use a fine mesh on the intake for greenhouse dust. Add printed feet (~8 mm) so the intake isn't blocked.
- **Exhaust on the side away from the handle.**
- **Port bezel:** cut a window in the Case Bottom side wall and screw a printed PETG bezel over it, so the shell isn't reprinted.
- **I/O strip** on the bar between the battery and the keyboard, so you can prototype without opening the case. Label the GPIO pins 3.3V.

**Lid:** 7" display centred in a redesigned Cover Top. The **USB Wi-Fi adapter + antenna** sits in the lid's right-side slot, high up for better range, on a short USB extension through the hinge. Use a matte anti-glare film and a panel with ≥ 400 nits.

## Carrying the Charger and IoT Kit

- **Store them in the base, under the keyboard (recommended).** Weight in the lid makes it tip back when open. Weight low in the base keeps the deck stable and balanced on the handle. Mount the keyboard on a lift-up tray (pin hinge at the I/O strip edge + 2 magnets at the front), or use a slide-out drawer through the front wall if the latches leave room.
- **Charger cradle:** a snug printed pocket with a strap or clip so the brick can't hit the keyboard underside. Coil its cable in a groove around it. Put the heaviest item near the handle side.
- **IoT kit tray:** a removable printed organizer with fitted pockets, lined with thin foam so nothing rattles:
  - half-size breadboard (≈ 82 × 55 × 9 mm)
  - 2× ESP32-S3 dev boards (pins pushed into foam or the breadboard)
  - jumper bundles (M-M, M-F) in a pouch
  - a few of the sensors you deploy (e.g., SHT45, soil moisture, light), in anti-static bags
  - short USB-C cable, small screwdriver
- **Weight check:** charger + kit ≈ 250–400 g. Weigh everything in Phase 11 against the 3 kg goal.
- **Fallback if the under-keyboard depth is too shallow** (< ~25 mm): put only light items (kit tray, ≤ 150 g) in a lid pocket with a door in Cover Top, close to the hinge, and keep the charger in the base.

## Field & Greenhouse Hardening

- **PLA softens around 55–60 °C.** Print the parts near heat (Cover Bottom, Jetson bracket, port bezel) in **PETG**.
- Silica-gel pouch in the base; let the deck warm up before opening after cold-to-warm moves.
- Intake mesh against dust; the lid closes over the keyboard.

## Local Coding Agent

No training happens on the deck or anywhere else: download a model that's **already tuned for coding and tool calling**, and run it under an agent tool.

- **Memory:** 8 GB is **shared** between the CPU and GPU, and the OS and desktop take ~1.5–2 GB. Agents also need a long context (system prompt + tool definitions + file contents), and that **KV cache** costs RAM on top of the weights. Budget ≤ 4 GB for model + context.
- **Model:** a **3B–4B instruct model with tool-calling support, at Q4** (~2–2.5 GB). Examples: Qwen2.5-Coder-3B-Instruct, Qwen3-4B, or whatever newer small agent-tuned coder is current when you set it up. A 1.5B model is good for autocomplete only. 7B won't fit with the context in 7 W mode.
- **Runtime:** Ollama, or `llama.cpp` `llama-server` with `--jinja` (enables tool calls). Set the context to **16k** and quantize the KV cache (q8_0) to save memory.
- **Agent front end:**
  - **Aider** (terminal): the most forgiving with small models. It edits files through diffs and runs your tests and linters.
  - **Continue (agent mode)** or **Cline** in VS Code: these need reliable tool calling, so test them with your chosen model.
- **Expectations:** a small local agent handles focused jobs well: writing a sensor script, fixing a bug in one file, explaining an error, writing a notebook cell. It won't match a cloud agent on multi-file refactors. Give it small, specific tasks, and use Claude Code when there's a connection.
- **Better results without training:** a project rules file (conventions, pinouts, your libraries), plus a docs folder of datasheets and notes the agent can search.