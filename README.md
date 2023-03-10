# XPS13-9360-Opencore
EFI for Opencore Hackintosh on Dell XPS 13 9360

## Related repos:

- https://github.com/jkbuha/XPS-9360-KabyLake-OpenCore
- https://github.com/the-darkvoid/XPS9360-macOS
- https://github.com/theQuert/XPS-9360-macOS


## System Specs:
- i7 7550U
- iGPU HD 620
- QHD Monitor
- Fenvi BCM94360ng from [here](https://de.aliexpress.com/item/32464748097.html?spm=a2g0o.store_pc_topSellerIng.8148356.26.3c362cf2tGldrX&pdp_npi=2%40dis%21EUR%21€%2072%2C37%21€%2039%2C08%21%21%21%21%21%4021038edf16784729040303144e2c59%2110000006058658845%21sh)

## Kexts (might be useful)
### Basics
- SMC..
  - Battery
  - DellSensors
  - LightSensor
  - Processor
  - SuperIO
  - VirualSMC
- Lilu
- AppleALC
  - layoutid: 0D000000
- Whatevergreen
  - AAPL,ig-platform-id: 00001659
  - device-id: 16590000
- USBToolBox & UTBMap

### Advanced
- BrightnesKeys
- ECEnabler
- FeatureUnlock
- HibernationFixup
- NVMEFix

### Cardreader
- https://github.com/0xFireWolf/RealtekCardReader
- https://github.com/acidanthera/EmeraldSDHC
- https://github.com/cholonam/Sinetek-rtsx

### Keyboard & Trackpad
- VoodooI2C
- VoodooI2CHID (touchscreen sleep issue fixed, so fully working)
- VoodooPS2Controller (delete VoodooInput from Plugins not to interfere with the one from VoodooI2C)

## BIOS
For undervolting max BIOS version is 2.13.0. I was able to downgrade from 2.21.0 by hitting F12 and Flash from USB.

**Don't** copy paste my VarStoreOffset, as these can differ on you machine. Changing something different might brick your machine, having to flash with somethink like a CH341A.

The get started, go ahead using Intel ME to get a biosreg.bin dump. The use UEFITool to get Section_PE32_image_Setup.sct.
TODO: Add more explanation...

<details> 
  <summary>BIOS Readouts</summary>
