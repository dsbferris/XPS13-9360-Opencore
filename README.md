# XPS13-9360-Opencore
OpenCore on Dell XPS 13 9360 \
Based on Dortania Guide and inspiration from the following repos.

## Related repos:

- https://github.com/jkbuha/XPS-9360-KabyLake-OpenCore
- https://github.com/the-darkvoid/XPS9360-macOS
- https://github.com/theQuert/XPS-9360-macOS


## System Specs:
| Type | Model |
| - | - |
| CPU | i7 7500U 2C/4T |
| RAM | 16 GB DDR3 |
| GPU | Intel HD 620 |
| Display | 13,3" Sharp SHP144 LQ133Z1 QHD+ (3200x1800) Touchscreen display |
| Wi-Fi | Fenvi BCM94360ng from [here](https://de.aliexpress.com/item/32464748097.html?spm=a2g0o.store_pc_topSellerIng.8148356.26.3c362cf2tGldrX&pdp_npi=2%40dis%21EUR%21€%2072%2C37%21€%2039%2C08%21%21%21%21%21%4021038edf16784729040303144e2c59%2110000006058658845%21sh) |
| Audio | ALC3246 (ALC256) |
| Cardreader | RTS525A |
| BIOS Version | 2.13.0 |

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
- OpenRuntime
- HfsPlus
- OpenCanopy
- OpenLinuxBoot
- ext4_x64

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
Try one of these. \
TODO: Benchmark/Test them all 

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

## Display Profiles
Thanks @[the-darkvoid](https://github.com/the-darkvoid/XPS9360-macOS)

Display profiles for the Sharp LQ133Z1 display (Dell XPS 9360 QHD+) are included in the displays folder.

Profiles can be installed by copying them into `/Users/<username>/Library/ColorSync/Profiles` folder, additionally the macOS built-in `ColorSync` utility can be used to inspect the profiles.

Profiles are configured on a per display basis in the `System Preferences` -> `Display` preferences menu.

## Useful Software
### macOS
- Stats
- Intel Power Gadget
- maciASL
- ProperTree (build the app from scripts folder, right click any plist file -> information -> set open with ProperTree)
- SSDTTime
- Karabiner Elements (keyboard mod for my qwertz to have all keys match)
- IORegExplorer
- MonitorControl (mostly for Desktops or dual monitor scenario)
- Endurance (stress test)
- DiffMerge (comparing configs)
- Pre-download XCode Commandline Tools with a free Apple Developer Account https://developer.apple.com/download/all/
- HomeBrew!!! with newest python, python-tk, 7z, smartmontools
- Having a full macOS offline installer at hand. Troubleshooting and redownloading from recovery every time ain't fun...

I actually don't use MountEFI, but rather do it myself with: 

diskutil list \
diskutil mount disk0s1 (adjust for yourself)


Credits to all the developers that made this possible!
