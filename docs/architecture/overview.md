flowchart LR
  phone[Smartphone App\nBLE Control] -- BLE --> mcu[Arduino Nano\nMCU & BLE Link]
  subgraph FW[Firmware]
    cmd[BLE Cmd Handler]
    anim[Animation Engine]
    fb[Frame Buffer]
  end
  mcu --> FW
  cmd --> anim --> fb
  fb --> drv[LED Drivers\n(shift regs / LED driver ICs)]
  drv --> mosfets[Transistor Arrays]
  mosfets --> cube[LED Cube Array (NxNxN)]

  subgraph PWR[Power 5 V / 3 A]
    jack[Input Jack]
    bulk[Bulk + Decoupling Caps]
  end
  jack --> bulk --> mcu
  bulk --> drv
  bulk --> cube

  mcu --- isp[Prog/Debug Header]
