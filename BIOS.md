- CFG Lock Offset 0x4DE 

  - 0x0 Disable
  - Default 0x1, Enabled
  
- DVMT Pre-Alloc 0x785 0x2 (64M) Default 0x1 (32M)

  - 0M = 0x0
  - 32M = 0x1
  - 64M = 0x2

- DVMT TOTAL 0x786 0x3 (MAX) Default ?

- Overclocking Lock 0x58D 

  - 0x0 Disable
  - Default 0x1 Enabled
  
- OverClocking Feature 0x64D

  - 0x1 Enabled 
  - Default 0x0 Disabled
  
- XTU Interface 0x64E

  - 0x1 Enable
  - Default 0x0 Disabled

- WDT Enable 0x89C Default 0x1

  - Disabled 0x0
  - Enabled 0x1
  
- Intel(R) Speed Shift Technology", Help: "Enable/Disable Intel(R) Speed Shift Technology support. Enabling will expose the CPPC v2 interface to allow for hardware controlled P-states.

  - VarStoreOffset: 0x4AD, Default 0x0
  - OneOfOption Option: "Disabled" Value: 0
  - OneOfOption Option: "Enabled" Value: 1

- Platform PL1 Enable 0x4CC, Default 0x0
Enable/Disable Platform Power Limit 1 programming. If this option is enabled, it activates the PL1 value to be used by the processor to limit the average power of given time window.

  - OneOfOption Option: "Disabled" Value: 0
  - OneOfOption Option: "Enabled" Value: 1

- Platform PL2 Enable 0x4D2, Default 0x0
Enable/Disable Platform Power Limit 2 programming. If this option is disabled, BIOS will program the default values for Platform Power Limit 2.

  - OneOfOption Option: "Disabled" Value: 0
  - OneOfOption Option: "Enabled" Value: 1 


-  AVX Ration Offset 0x658 Default 0x0

  - 0xY, Y=negativ offset, 0<=Y<=31

- Core Max OC Ratio 0x64F Default 0x0

  - Sets the maximum OC Ratio for the CPU Core and Ring. Uses Mailbox MSR 0x150, cmd 0x10, 0x11. Range 8-83. 0 is AUTO.

- Core Voltage Offset Prefix 0x655 Default 0x0
  - "+ 0x0"
  - "- 0x1"

- Core Voltage Offset 0x653 (eg 0x64 = 100mV) Default 0x0
Specifies the Offset Voltage applied to the IA Core domain. This voltage is specified in millivolts. Uses Mailbox MSR 0x150, cmd 0x11. Range -500 to 500 mV


- GT Voltage Offset Prefix 0x85C Default 0x0
  - "+ 0x0"
  - "- 0x1"

- GT Voltage Offset 0x85A (eg 0x1E = 30mV) Default 0x0
Specifies the Offset Voltage applied to the GT domain. This voltage is specified in millivolts. Uses Mailbox MSR 0x150, cmd 0x11. Range -1000 to 1000 mV
