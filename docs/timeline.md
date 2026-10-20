# Timeline

8 weeks, **19 Oct – 13 Dec 2026**. Each row maps to the phases and goals in [todos.md](todos.md).

| Week | Dates | Phases | Goal | Milestone |
| ---- | ----- | ------ | ---- | --------- |
| 1 | Oct 19 – Oct 25 | 0 Mission · 1 Requirements · 2 Architecture | Purpose, project goals and requirements frozen | **Parts ordered by Oct 23** |
| 2 | Oct 26 – Nov 1 | 2 Architecture · 5 CAD (modeling) | Block diagrams, wiring diagram, BOM; every component measured or modeled | Architecture complete |
| 3 | Nov 2 – Nov 8 | 3 Bring-up · 7 Power · 6 Thermal · 10 OS · 4 LLM | Jetson running on the 5V → boost chain, display and Wi-Fi working, power measured | ✅ **Go / no-go gate** |
| 4 | Nov 9 – Nov 15 | 5 CAD (layout) · 6 Thermal · 4 LLM | Full CAD: Cover Bottom, port bezel, I/O strip, keyboard tray, storage bay, Cover Top | CAD assembly complete |
| 5 | Nov 16 – Nov 22 | 8 Test prints · 4 Agent setup · 13 Paper plan | Tolerances verified; Aider/Continue running on the local model; paper outline | Prototype parts fit |
| 6 | Nov 23 – Nov 29 | 8 Final prints · 4 Agent evaluation · 13 Draft | All PETG parts printed; best model + agent combination chosen from real tasks | Printed parts finished |
| 7 | Nov 30 – Dec 6 | 9 Assembly · 10 Software · 13 Draft | Deck assembled with charger and IoT kit inside; analysis + IoT software ready | Hardware assembled |
| 8 | Dec 7 – Dec 13 | 11 Testing (Mon–Thu) · 12 Refinement & docs (Fri–Sat) · 13 Paper final (Sun) | Every project goal measured; fixes and docs done; validation section written | **Project complete + paper draft, Dec 13** |

### Critical path

`Order parts (Oct 23) → Bench gate (Nov 8) → CAD (Nov 15) → Prints (Nov 29) → Assembly (Dec 6) → Testing (Dec 10)`

- **Shipping is the biggest risk.** If the Jetson arrives late, start the CAD from NVIDIA's published dev-kit 3D model and keep the LLM and paper tracks going (they don't need the hardware until benchmarking).
- **If the Week 3 gate fails** (brownouts on the 5V boost path, or no image on the display), fix it in week 4 alongside CAD. The fallback for power is a 12V USB-C PD trigger; nothing else in the layout changes.
- **Paper sections that don't need test data** (context, description, design files, BOM, build) are drafted in weeks 6–7, so week 8 only adds the validation results.
