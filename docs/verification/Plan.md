# Verification Plan — 8x8x8 LED Cube

## 1. Strategy
Verify animation, PWM, BLE control, reliability, power, and layout by visual tests, current and temperature measurements, and checklists. Link evidence per TestID.

## 2. Equipment
- 5 V / 3 A PSU
- Smartphone camera (30–60 fps; slow-mo is available)
- Multimeter with current range and thermometer probe
- Phone BLE app (your tool)

## 3. Tests and Procedures

### Functional
- **ST-SYS-001 ↔ SYS-F1 — Smooth motion ≥60 fps (perceived)**
  - Play fast sweep. Film at 60 fps from 0.5–1 m. Pass: no visible flicker/banding.
- **ST-SYS-002 ↔ SYS-F2 — 8-bit PWM monotonic**
  - Drive single voxel through 16 steps (0,17,…,255). Record video. Pass: brightness increases monotonically.
- **ST-SYS-003 ↔ SYS-F3 — Presets in MCU flash**
  - Build ≥5 presets totaling ≥16 kB. Show selection playback. Add linker map table.
- **ST-IFC-004 ↔ SYS-F4 — BLE link + command**
  - Send PLAY/PAUSE/SET_BRIGHT from phone. Record screen + cube. Pass: action within 300 ms.
- **ST-IFC-005 ↔ SYS-F5 — Command matrix over BLE**
  - Exercise PLAY, PAUSE, SET_BRIGHT, SELECT_ANIM, UPLOAD_PRESET. Log inputs/observed outputs.
- **ST-TOOLS-006 ↔ SYS-F6 — Stream E2E**
  - Convert short animation on phone and stream. Pass: visual matches reference; transfer completes without disconnects.

### Non-functional
- **ST-PWR-101 ↔ SYS-N1 — Peak/steady current ≤ 3.0 A**
  - Put meter in series at PSU output. Run full-white 10 s. Record steady current. Pass: ≤ 3.0 A. Note PSU rating if peaks unknown.
- **ST-REL-102 ↔ SYS-N2 — 2 h run; Tcase ≤ 70 °C**
  - Tape probe to hottest device (MOSFET/PNP or regulator). Run mixed patterns 2 h at room temp. Log temp every 15 min. Pass: ≤ 70 °C; no resets/disconnects.
- **ST-SCM-103 ↔ SYS-N3 — BOM alternates**
  - For MCU, shift register, high-side switch: list two purchasable alternates with links. Pass: documented.

### Hardware
- **ST-HW-201 ↔ HW-1 — Column chain check**
  - Run walking-1 pattern per column. Confirm all 64 columns in order on each layer. Note any missing/swapped.
- **ST-HW-202 ↔ HW-2 — High-side N-MOS sizing**
  Compute worst-case sink current = 64 × I_LED × duty. Full-white test; spot-check MOSFET case temperature. Pass: calc documented; Tcase < 70 °C.
- **ST-HW-203 ↔ HW-3 — Column current limit (N-MOS sinks)**
  Light a single voxel; estimate I_LED from PSU current delta. Cross-check R value: R ≈ (5 V − V_F(LED) − I_LED·R_DS(on)) / I_LED. Pass: measurement.txt + resistor calc.
- **ST-HW-204 ↔ HW-4 — Decoupling/bulk audit**
  - Checklist + photos: 0.1 µF per IC; 1 µF per 2–4 ICs; bulk at input. Pass: placements present and near pins.
- **ST-HW-205 ↔ HW-5 — Input protection**
  - If fitted: photo + part ratings. If omitted: exception note with connector/handling controls. Pass: one of the two recorded.

  ### PCB checks
- **ST-PCB-301 ↔ HW-6 — ERC clean**
  KiCad ERC with zero errors; intentional warnings documented. Pass: ERC report PDF and screenshot.
- **ST-PCB-302 ↔ HW-6 — DRC clean per rules**
  Set rules per docs/PCB.md; run DRC; zero errors. Pass: DRC report PDF and screenshot.
- **ST-PCB-303 ↔ HW-8 — Fab package completeness**
  Generate Gerbers, drill, IPC-356, PDFs, BoM, PnP; open in a Gerber viewer to spot check. Pass: Zip list + viewer screenshots.
- **ST-PCB-304 ↔ HW-7 — Test pads present**
  Mark and photograph all required pads; continuity check to nets. Pass: Board photos and annotated image.
- **ST-PCB-305 ↔ HW-2/HW-4 — Copper and gate control sanity**
  Document ground return widths from layer N-MOSFETs to input ground; show current density rationale.

## 4. Evidence
Store videos, photos, logs under `docs/verification/data/`. Summaries in `docs/verification/Reports.md` with anchors per TestID.

## 5. Exit Criteria
All tests executed. Failures resolved or justified in report. Traceability updated.
