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

  fb --> drv["LED Drivers / Shift Regs"]
  drv --> sinks["Low-side Sinks<br/>ULN2803A or MOSFETs"]
  sinks --> cube["LED Cube Array<br/>(N×N×N)"]

  subgraph PWR[Power 5 V / 3 A]
    jack["Input Jack / USB-C"]
    bulk["Bulk + Decoupling Caps"]
  end
  jack --> bulk --> mcu
  bulk --> drv
  bulk --> cube

  mcu --- isp["Prog/Debug Header"]
