# System Requirements Specification — 8x8x8 LED Cube

## 1. Scope
An 8x8x8 monochrome LED cube with per-voxel PWM, multiplexed layers, scripted animations, and smartphone control via Bluetooth Low Energy (BLE). Target electronics cost ≤ €100.

## 2. Stakeholders
Builder/Owner: single developer. Audience: recruiters.

## 4. System Overview
An Arduino nano MCU drives 8 layers through high-side switches and 64 columns via shift registers. PWM in a timer ISR. Control and animation upload over BLE. 5 V / 3 A supply.

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
- **HW-2**: 8 high-side switches (P-MOS or PNP) sized for worst-case layer current = 64 × I_LED × duty; gate/base resistors; flyback only if inductive paths exist.
- **HW-3**: Per-column resistors for 10–15 mA LED current (per LED Vf).
- **HW-4**: Decouple each driver IC; bulk capacitance at input.
- **HW-5**: Input protection: reverse-polarity element and ≥ 5 A fuse/polyfuse; optional

