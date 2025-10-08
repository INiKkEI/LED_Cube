# High-Level Architecture

```mermaid
flowchart LR
  phone["Smartphone App<br/>BLE Control"] -- BLE --> mcu["Arduino Nano<br/>MCU & BLE Link"]

  subgraph FW[Firmware]
    cmd[BLE Cmd Handler]
    anim[Animation Engine]
    fb[Frame Buffer]
  end
  mcu --> FW
  cmd --> anim --> fb

  fb --> drv["Shift Regs"]
  drv --> sinks["MOSFETs"]
  sinks --> cube["LED Cube Array<br/>(8×8×8)"]

  subgraph PWR[Power 5 V / 3 A]
    jack["Input Jack"]
    bulk["Bulk + Decoupling Caps"]
  end
  jack --> bulk --> mcu
  bulk --> drv
  bulk --> cube

  mcu --- isp["Prog/Debug Header"]
