# 🧾 Bill of Materials

Tracks what's on hand, what still needs buying, and what it all costs.

**How to use it**
- **Status:** `Have` → already owned · `Need` → still to buy · `Ordered` → bought, on the way · `Received` → arrived and checked.
- **Price:** `paid` = what you actually paid · `est.` = estimate, to be replaced with the real price when you order.
- **Weight (g):** weigh each part when it arrives. The total checks the ≤ 3 kg goal and goes into the paper.
- When a price changes, update the item row, its section subtotal and the summary at the bottom.

---

## Summary

| Section | Have (US$) | Need (US$) |
| ------- | ---------: | ---------: |
| A. Compute & Storage | 17.66 | 289.00 |
| B. Display & Input | 10.99 | 80.00 |
| C. Power | 24.99 | 54.00 |
| D. Connectivity & I/O | 17.68 | 20.00 |
| E. Mechanical & Printing | 13.99 | 48.00 |
| F. IoT Prototyping Kit | 0.00 | 56.00 |
| **Total** | **85.31** | **547.00** |

**Whole project (have + need): US$ 632.31** · Budget goal: ~US$ 500

> ⚠️ The parts still to buy (estimates) come to about US$ 47 over the budget, before counting what you already own. Ways to close the gap:
> - Use spare sensors from the greenhouse instead of buying F4–F6 (−18)
> - Get a 256GB NVMe instead of 512GB (≈ −15)
> - Skip the anti-glare film until field testing shows you need it (−8)
> - Borrow an inline USB power meter instead of buying one (−15)

---

## A. Compute & Storage

| # | Item | Qty | Status | Unit (US$) | Total (US$) | Price | Weight (g) | Source / Notes |
| - | ---- | --: | ------ | ---------: | ----------: | ----- | ---------: | -------------- |
| A1 | NVIDIA Jetson Orin Nano 8GB Super Developer Kit | 1 | Have | 300.00 | 300.00 | paid | | Includes heatsink, fan and Wi-Fi/BT card |
| A2 | NVMe SSD 256GB, M.2 2280 | 1 | Need | 42.29 | 42.29 | est. | | OS + models |
| A3 | External HD 256GB | 1 | Have | 0 | 0 | paid | | Datasets in and out (Optional) |
| A4 | microSD card 64GB | 1 | Have | 24.99 | 24.99 | paid | | Recovery / flash image |
| | **Subtotal** | | | | **Have 324.99 · Need 42.29** | | | |

## B. Display & Input

| # | Item | Qty | Status | Unit (US$) | Total (US$) | Price | Weight (g) | Source / Notes |
| - | ---- | --: | ------ | ---------: | ----------: | ----- | ---------: | -------------- |
| B1 | 7" IPS HDMI display, USB touch, ≥ 400 nits, 1280×800 | 1 | Need | 50.00 | 50.00 | est. | | Avoid 1024×600; buy from a seller with returns |
| B2 | DisplayPort → HDMI adapter (passive) | 1 | Need | 10.00 | 10.00 | est. | | |
| B3 | Slim FPC HDMI cable 30–50 cm + angle adapters | 1 | Need | 12.00 | 12.00 | est. | | Runs through the hinge |
| B4 | Ultra-thin USB mini wired keyboard (11.2") | 1 | Have | 10.99 | 10.99 | paid | | |
| B5 | Matte anti-glare screen film, 7" | 1 | Need | 8.00 | 8.00 | est. | | Optional |
| | **Subtotal** | | | | **Have 10.99 · Need 80.00** | | | |

## C. Power

| # | Item | Qty | Status | Unit (US$) | Total (US$) | Price | Weight (g) | Source / Notes |
| - | ---- | --: | ------ | ---------: | ----------: | ----- | ---------: | -------------- |
| C1 | Power bank 10,000 mAh with pass-through | 1 | Have | 24.99 | 24.99 | paid | | Check the label: 5V output per port, input rating |
| C2 | Outlet charger | 1 | Have | — | — | paid | | Check it's ≥ 20 W |
| C3 | Boost converter 5V → 12V, rated ≥ 24 W | 1 | Need | 10.00 | 10.00 | est. | | Not a 1 A "USB to 12V" cable |
| C4 | USB-C 5V breakout with 5.1 kΩ CC resistors | 1 | Need | 4.00 | 4.00 | est. | | Makes the bank turn on its 5V |
| C5 | Panel-mount USB-C extension | 1 | Need | 8.00 | 8.00 | est. | | The single power input |
| C6 | Latching power switch, panel mount, ≥ 5 A | 1 | Need | 3.00 | 3.00 | est. | | |
| C7 | Inline fuse holder + 4 A fuses | 1 | Need | 4.00 | 4.00 | est. | | |
| C8 | Electrolytic capacitor 2200 µF 25 V | 1 | Need | 1.00 | 1.00 | est. | | Rides through pass-through dropouts |
| C9 | 5.5 × 2.5 mm barrel plug pigtail | 1 | Need | 3.00 | 3.00 | est. | | To the Jetson |
| C10 | 18 AWG wire + heat-shrink | 1 | Need | 6.00 | 6.00 | est. | | |
| C11 | Inline USB power meter | 1 | Need | 15.00 | 15.00 | est. | | For runtime / power tests |
| | **Subtotal** | | | | **Have 24.99 · Need 54.00** | | | |

## D. Connectivity & I/O

| # | Item | Qty | Status | Unit (US$) | Total (US$) | Price | Weight (g) | Source / Notes |
| - | ---- | --: | ------ | ---------: | ----------: | ----- | ---------: | -------------- |
| D1 | USB Wi-Fi adapter with external antenna | 1 | Have | 4.99 | 4.99 | paid | | Check the ARM64 driver in Phase 3 |
| D2 | 7-port USB hub | 1 | Have | 12.69 | 12.69 | paid | | Feeds the HD + I/O strip |
| D3 | Short USB-A extension (~30 cm) | 1 | Need | 5.00 | 5.00 | est. | | Wi-Fi adapter in the lid |
| D4 | 40-pin GPIO ribbon cable + breakout board | 1 | Need | 8.00 | 8.00 | est. | | I/O strip |
| D5 | Qwiic / STEMMA QT cable or adapter | 1 | Need | 4.00 | 4.00 | est. | | I²C jack on the I/O strip |
| D6 | USB-A → USB-C adapter | 1 | Need | 3.00 | 3.00 | est. | | Only if the hub's upstream plug is USB-C |
| | **Subtotal** | | | | **Have 17.68 · Need 20.00** | | | |

## E. Mechanical & Printing

| # | Item | Qty | Status | Unit (US$) | Total (US$) | Price | Weight (g) | Source / Notes |
| - | ---- | --: | ------ | ---------: | ----------: | ----- | ---------: | -------------- |
| E1 | Printed shell: Case Top/Bottom, Handle, 2× Latch Arm, 2× Latch Cam, Hinge Pin | 1 set | Have | — | — | paid | | Cost included in E2 |
| E2 | PLA filament 1 kg | 1 | Have | 13.99 | 13.99 | paid | | |
| E3 | PETG filament 1 kg | 1 | Need | 20.00 | 20.00 | est. | | Cover Bottom, bezel, Jetson bracket |
| E4 | M3 bolts (15) + M3 nuts (2) | 1 set | Have | — | — | paid | | |
| E5 | M3 heat-set inserts (extra for new parts) | 1 pack | Need | 8.00 | 8.00 | est. | | |
| E6 | Magnets 6 × 3 mm | 1 pack | Need | 5.00 | 5.00 | est. | | Keyboard tray |
| E7 | Fine dust mesh | 1 | Need | 5.00 | 5.00 | est. | | Intake grille |
| E8 | Silica-gel packs | 1 pack | Need | 5.00 | 5.00 | est. | | |
| E9 | Thin foam sheet | 1 | Need | 5.00 | 5.00 | est. | | IoT kit tray lining |
| | **Subtotal** | | | | **Have 13.99 · Need 48.00** | | | |

## F. IoT Prototyping Kit

| # | Item | Qty | Status | Unit (US$) | Total (US$) | Price | Weight (g) | Source / Notes |
| - | ---- | --: | ------ | ---------: | ----------: | ----- | ---------: | -------------- |
| F1 | ESP32-S3 dev board | 2 | Need | 10.00 | 20.00 | est. | | |
| F2 | Half-size breadboard | 1 | Need | 4.00 | 4.00 | est. | | |
| F3 | Jumper wire kit (M-M, M-F) | 1 | Need | 7.00 | 7.00 | est. | | |
| F4 | SHT45 temperature / humidity breakout | 1 | Need | 12.00 | 12.00 | est. | | Or a spare from the greenhouse |
| F5 | Capacitive soil moisture sensor | 1 | Need | 3.00 | 3.00 | est. | | Or a spare from the greenhouse |
| F6 | BH1750 light sensor | 1 | Need | 3.00 | 3.00 | est. | | Or a spare from the greenhouse |
| F7 | Anti-static bags | 1 pack | Need | 3.00 | 3.00 | est. | | |
| F8 | Short USB-C cable | 1 | Need | 4.00 | 4.00 | est. | | Flashing ESP32s |
| | **Subtotal** | | | | **Have 0.00 · Need 56.00** | | | |

---

## Weight Check (fill in as parts arrive)

| Group | Weight (g) |
| ----- | ---------: |
| Shell + printed parts | |
| Electronics (A–D) | |
| Charger + cable | |
| IoT kit (F) | |
| **Total** (goal ≤ 3000 g) | |
