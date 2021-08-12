# hackintosh-msi-gf638rd
Hackintosh EFI OpenCore BigSur (Update from Catalina) for MSI laptop, with OLARILA



#  MSI GF63 8RD Hackintosh Laptop
This hackintosh is for MSI GF63 8RD, WIFI WORK using Heliport, HDMI working, sound working using map = 8, may different than other MSI GF638 RD
This is an OpenCore 0.7.1 install for Catalina then updated to MacOS Big Sur 11.5. This build initially a triple boot but then remove, only OpenCore data that can be copied into EFI Folder you have.

### MSI GL72M 7RDX Laptop 
| :computer: Specifications | :thumbsup: Functioning Components | :no_entry: Non-Functioning Components |
|--|--|--|
| Intel UHD 630 | :white_check_mark: Intel UHD 630 2048 mb working |  |
| GeForce® GTX 1050Ti with Max-Q Design, 4GB GDDR5 |  | :x: nVidia GTX 1050 |
| Intel® HM370 chipset | :white_check_mark: USB C/3.0 | :x: Sleep/Wake functionality (only lock) |
| Realtek ALC269 | :white_check_mark: Audio (ALCID=8) | |
| 15.5" UHD display 1920x1080 | :white_check_mark: Screen brightness adjustment  | |  
| 12gb 2400mhz DDR4 (Upgraded) |  | |
| WDC PC SN520 SDAPNUW-256G SSD | :white_check_mark: Microphone | |
| 2TB HDD SEAGATE (upgraded) | :white_check_mark: Webcam | |
| Intel Wireless   | :white_check_mark: Wifi using HeliPort | :x: iMessage/Facetime |
| Core i7-8750H | :white_check_mark: Ethernet port | |
| Backlight Keyboard (Single-Color, Red) | :white_check_mark: Keyboard brightness | |
| HDMI | :white_check_mark: HDMI |  |
|[Manufacturers Website](https://www.msi.com/Laptop/GF63-8RD/Specification) | | |


## :muscle: Upgrades

### HDD 2 TB Seagate for Data
Initially use 2TB for boot, but the performance was poor, and change using SSD built-in MSI, side by side with Windows 10 OEM, and performance increasingly significant, it is like 10x!, 

**Some options only available in advanced mode:**\
In BIOS, holding **ALT + RIGHT-CTRL + SHIFT** together then press **F2**

| Settings |  |
|--|--|
| `CFG Lock` | Disable |
| `CSM` | Disable |
| Fast Boot | Disable |
| `Intel Speed Shift`(aka. HWP) | Enable |
| Secure Boot | Disable |
| Enable Hiberation | Disable |
| DVMT Pre-Allocated | 64M |

<pre>
[Advanced] tab
├─ Power & Performance
│  └─ CPU-Power Management Control
│     ├─ <b>Intel(R) Speed Shift Technology</b>
│     └─ CPU Lock Configuration
│        └─ <b>CFG Lock</b>
├─ System Agent (SA) Configuration
│  └─ Graphics Configuration
│     └─ DVMT Pre-Allocated
├─ CSM Configuration
│  └─ <b>CSM Support</b>
│   
└─ ACPI Settings
   └─ <b>Enable Hibernation</b>
</pre>

## :notebook_with_decorative_cover: Installation Notes

### ACPI Patching Notes
THIS ACPI patch use multiple source information from Internet, and use OLARILA DSDT to Boot from CATALINA, (UNABLE TO DIRECTLY INSTALL BIG SUR!) after update into BIGSUR, audio only work using APPLEALC, and luckily i get map id (8) and work! may be different than yours!.

### Fixing the framebuffer
FIXING FRAMEBUFFER USING HACKINTOOLS and boot-flag is to get HDMI and sleep/lock working (The issue initially arise before i get them to fix is blank screen, and find out to patch them based on reddit, github, olarilla and other source, keep digging and searching for hackintosher!

### Wifi on Big Sur
Only work using itwlm instead airport, so that Heliport is mandatory!, need to work around for this to have default wifi work!

### Getting the touchpad and buttons to function
I just had to use an older Rehabman kext instead of the latest version. 

### Source and credit
This hackintosh EFI using multiple sources, and i may forget to add thanks to github! Olarila! clover! opencore! always give best hint!
- https://github.com/jbwharris/hackintosh-msi-GL72M-7RDX
- https://github.com/johnnync13/XiaomiGaming
- https://www.olarila.com
- https://dortania.github.io/OpenCore-Install-Guide/ (JUST don't forget for MSI OEM - EnableWriteUnprotector set to YES!) to avoid boot failed - framelimit buffer , etc and look at the detail from dortania:
-  -- "However, due to issues with OEMs not using the latest EDKII builds you may find that the above combo will result in early boot failures. This is due to missing the MEMORY_ATTRIBUTE_TABLE and such we recommend disabling RebuildAppleMemoryMap and enabling EnableWriteUnprotector. More info on this is covered in the troubleshooting section". 

## ENJOY!
![alt text](https://raw.githubusercontent.com/IqbalF69/hackintosh-msi-gf638rd/main/2021-08-12_12-35_1.png)
