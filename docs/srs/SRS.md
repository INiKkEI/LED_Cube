# System Requirements Specification — 8x8x8 LED Cube

## 1. Scope
An 8x8x8 monochrome LED cube with per-voxel PWM, multiplexed layers, scripted animations, and smartphone control via Bluetooth Low Energy (BLE). Target electronics cost ≤ €100.

## 2. Stakeholders
Builder/Owner: single developer. Audience: recruiters.

## 4. System Overview
An Arduino Nano MCU drives 8 layers via low-side N-MOSFETs whose gates come from an 8-bit shift register; 64 columns come from a 64-bit shift-register chain. PWM in a timer ISR. BLE control. 5 V / 3 A supply

## 5. Functional Requirements
- **SYS-F1**: Display static and animated 3D frames at ≥ 60 fps perceived.
- **SYS-F2**: Per-voxel PWM with 8-bit effective depth.
- **SYS-F3**: Store and play animations from internal MCU flash only; ≥ 5 presets totaling ≥ 16 kB.
- **SYS-F4**: Accept frames/commands over BLE.
- **SYS-F5**: Commands: play, pause, set global brightness, select animation, upload preset.
- **SYS-F6**: Phone tool converts assets to on-cube format and streams via BLE.

## 6. Non-functional Requirements
- **SYS-N1**: Peak input current ≤ 3.0 A at full white, 25 °C.
- **SYS-N2**: Continuous run 2 h at 25 °C without resets; max device case temp ≤ 70 °C.
- **SYS-N3**: BOM resilience; two alternates for each critical part.

## 7. Hardware Requirements
- **HW-1**: 64 column drivers via SPI daisy-chained shift registers with latch and OE.
- **HW-2**: 8 low-side N-MOSFET layer switches, each sized to sink worst-case layer current = 64 × I_LED × duty. Use logic-level MOSFETs with low R_DS(on) at V_GS=5 V; add 22–100 Ω gate resistors and ~100 kΩ gate pulldowns. Gates are driven by a dedicated 8-bit shift register with latch; timing coordinated with OE blanking. 
- **HW-3**: Per-column resistors for 10–15 mA LED current (per LED Vf).
- **HW-4**: Decouple each driver IC; bulk capacitance at input.
- **HW-5**: Input protection: reverse-polarity element and ≥ 5 A fuse/polyfuse; optional
- **HW-6 (PCB rules)**: 2-layer FR-4, 1 oz Cu, min clearance ≥ 0.2 mm, min track ≥ 0.25 mm (signals), power nets ≥ 1.0 mm; via drill ≥ 0.6 mm for power trunks.
- **HW-7 (Testability)**: Provide labeled test pads for +5V, GND, OE, LATCH, SCK, MOSI, and two LAYER_EN lines; silkscreen pin map and polarity marks.
- **HW-8 (Fabrication package)**: Provide Gerbers, drill files, IPC-356 netlist, PDF schematic, PDF assembly drawing, BoM CSV, and pick-and-place CSV.


