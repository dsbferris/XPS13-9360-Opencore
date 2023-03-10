# XPS13-9360-Opencore
EFI for Opencore Hackintosh on Dell XPS 13 9360
Based on Dortania Guide and inspiration from the following repos.

## Related repos:

- https://github.com/jkbuha/XPS-9360-KabyLake-OpenCore
- https://github.com/the-darkvoid/XPS9360-macOS
- https://github.com/theQuert/XPS-9360-macOS


## System Specs:
- i7 7550U
- iGPU HD 620
- QHD Monitor
- Fenvi BCM94360ng from [here](https://de.aliexpress.com/item/32464748097.html?spm=a2g0o.store_pc_topSellerIng.8148356.26.3c362cf2tGldrX&pdp_npi=2%40dis%21EUR%21€%2072%2C37%21€%2039%2C08%21%21%21%21%21%4021038edf16784729040303144e2c59%2110000006058658845%21sh)

SMBIOS: MacBookPro14,1

Thunderbolt not tested.

Triple-boot of :
- macOS Ventura 13.2.1
- Ubuntu
- Windows 11

## ACPI
### With SSDTTime
- EC
- PLUG
- PNLF
- XOSI
- USBX

### Ripped or done manually
- All the others ;)

TODO: Specify more

## Drivers
- ext4_x64 (dunno why, maybe it was neccessary)
- HfsPlus
- OpenCanopy
- OpenLinuxBoot
- OpenRuntime

## Tools
- CleanNvram
- ControlMsrE2
- OpenShell
- setup_var (I threw it in there, can by anywhere else. See BIOS Modding for use)

## Resources
BlackOSX/BsxM1 - looks very sexy ;)

## Kexts
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
  - device-id: 16590000 (I think adding this resolved USB-C->HDMI output issue)
  - You might need some more framebuffer patching, if you are not going to change DVMT in the bios.
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

## Config
Additionally I did (more like ripped) the following:

Wakeup from keypress
PciRoot(0x0)/Pci(0x14,0x0) -> acpi-wake-type -> Data [01]

## BIOS Settings
TODO

## BIOS Modding
To unlock undervolting max BIOS version is 2.13.0. Search "Plundervolt" to see why it has been locked with future BIOS updates.
I was able to downgrade from 2.21.0 by hitting F12 and Flash from USB.

**DONT** simply copy paste my VarStoreOffset, as these can differ on you machine. Changing something different might brick your machine, having to flash with somethink like a CH341A.

To get started, go ahead using Intel ME to get a biosreg.bin dump. Then use [UEFITool](https://github.com/LongSoft/UEFITool) to get Section_PE32_image_Setup.sct. Then use ifrextract to get the text file containing the informations I noted down in BIOS.md.
Write down your offsets and possible values.
From Opencore run OpenShell and run https://github.com/datasone/setup_var.efi to change your values.

TODO: Add more explanation
TODO: Add which parameters I changed

## Undervolting
- Windows: ThrottleStop/XTU
  - I prefer ThrottleStop. XTU Version 6.5.2.40 recommended. https://www.computerbase.de/downloads/systemtools/intel-extreme-tuning-utility-xtu/
- macOS: https://github.com/sicreative/VoltageShift
- Ubuntu: https://github.com/georgewhewell/undervolt

On my machine -90mV on everything seems fine.

## Hardware tuning
I did a fresh thermal paste application.
I generously added Thermalpads onto the heatpipe to make contact with the backplate.
I added a bit of kapton tape to close the gap between the fan and the heatpipe. This hopefully prevents hot air getting back inside the case instead of being blown out. Before I got myself some kapton tape I used casual masking tape, which turned out to be fine, but you might risk the adhesive melting under higher temperatures.

TODO: Add images

With the undervolting and hardware tuning combined, this thing can easily boost all day at turbo clock speed.


Credits to all the developers that made this possible!
