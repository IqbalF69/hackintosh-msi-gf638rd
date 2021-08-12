# hackintosh-msi-gf638rd
Hackintosh EFI OpenCore BigSur (Update from Catalina) for MSI laptop, with OLARILA

This hackintosh is for MSI GF63 8RD, WIFI WORK using Heliport, HDMI working, sound working using map = 8, may different than other MSI GF638 RD
💻 Specifications	👍 Functioning Components	⛔ Non-Functioning Components
Intel HD 630	✅ Intel HD 630 1536mb working	❌ nVidia GTX 1050
GeForce® GTX 1050 with 2GB GDDR5	✅ Wifi	❌ SD card reader
Intel® HM175 chipset	✅ USB C/3.0	
Realtek ALC898	✅ Ethernet port	
17.3" HD display 1920x1080	✅ Audio	
16gb 2400mhz DDR4	✅ Microphone	
250GB WD Blue 3D NAND PC SSD	✅ iMessage/Facetime	
1TB ADATA SU800 SSD	✅ Sleep/Wake functionality	
Broadcom DW1820A BCM94350ZAE	✅ Keyboard brightness	
Core i7 7700HQ	✅ Screen brightness adjustment	
Backlight Keyboard (Single-Color, Red)	✅ Webcam	
HDMI	✅ HDMI	
Mini Display Port	✅ Mini Display Port	
Manufacturers Website	✅ Ethernet through USB C	
💪 Upgrades
Wifi Card
I purchased a Broadcom DW1820A BCM94350ZAE 2.4G/5G Dual Band 867Mbps M.2 NGFF WiFi Card with Bluetooth 4.1 and swapped it into the laptop.

USB C Hub
Hub works and allows me to plugin additional USB items and read SD cards, but HDMI passthrough do not work. The ethernet connection does work, so I can just plugin the hub and be connected to a wired connection automatically.

WD Blue 3D NAND 250GB PC SSD - SATA III 6 Gb/s M.2 2280 Solid State Drive
Main boot drive for this machine.

1TB ADATA SU800 SSD
Windows and Ubuntu run off this drive, as well as a clone of the main SSD.

👴 BIOS Configuration
The section below adapted from @0ranko0P's MSI-GL62M 7RD Hackintosh. This was huge, as I never knew how to access all the advanced settings in my BIOS.

Some options only available in advanced mode:
In BIOS, holding ALT + RIGHT-CTRL + SHIFT together then press F2

Settings	
CFG Lock	Disable
CSM	Disable
Fast Boot	Disable
Intel Speed Shift(aka. HWP)	Enable
Secure Boot	Disable
Enable Hiberation	Disable
DVMT Pre-Allocated	64M
[Advanced] tab
├─ Power & Performance
│  └─ CPU-Power Management Control
│     ├─ Intel(R) Speed Shift Technology
│     └─ CPU Lock Configuration
│        └─ CFG Lock
├─ System Agent (SA) Configuration
│  └─ Graphics Configuration
│     └─ DVMT Pre-Allocated
├─ CSM Configuration
│  └─ CSM Support
│   
└─ ACPI Settings
   └─ Enable Hibernation
📔 Installation Notes
ACPI Patching Notes
This laptop already has an embedded controller named EC in the DSDT, so it doesn't need to be patched.

USB Port Limit
I used Hackintool to fix my USB ports, along with a few other issues. It generated a new USBPorts.kext for my system and installed it in kexts/other. This iteration removes the MSI EPF USB and USB2.0-CRW SD Card Reader, as they serve no purpose.

Fixing the framebuffer
This has been the bane of my existence when it comes to this laptop. I finally got it working with OpenCore after ages of messing around with Hackintool patches, Skylake spoofs(that previously worked in Clover) and other people's MSI laptop setups. After recently learning how to access the BIOS settings to change the DVMT Pre-Allocated to 64m, which then allowed me to remove the 32mb DVMT-prealloc patches. Then after much trial and error, instead of using the 2 Intel HD Graphics 630 listed under Kaby Lake in the laptop guide, I tried the Unlisted GPU 05001c59 mentioned right below them and now the LVDS screen no longer has a flicker.

Bluetooth using DW1820A BCM94350ZAE
I have struggled for a long time with getting the Bluetooth to work on this laptop. The thing that finally worked for me was adding 'bpr_probedelay=200 bpr_initialdelay=400 bpr_postresetdelay=400' to my boot-args. Revised solutions to DW1820A support

Wifi using DW1820A BCM94350ZAE on Big Sur
After getting Big Sur to work on my machine the biggest issue was getting the wifi to actually work. I had to set a boot-arg to brcmfx-driver=2 and change the entry in for AirPortBrcm4360_Injector.kext to MaxKernel 19.9.9. That's all in the OpenCore Guide, but thought it worth flagging.

Getting the touchpad and buttons to function
@kOOsi3 pointed out a solution to getting the touchpad to work. I just had to use an older Rehabman kext instead of the latest version.

🤦‍♂️ Outstanding Issues
Flat audio through USB
I've noticed this issue lately where the audio coming through the USB C hub to my Creative speakers is really flat sounding. Then when the laptop screen goes to sleep, it'll go back to sounding good, then when woken up it's flat again. When connected via Bluetooth it sounds great, but then I can't actually push audio out to it at the same time as my Airplay speakers. Still trying to figure out an ideal solution there.

