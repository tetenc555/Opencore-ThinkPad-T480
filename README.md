<!-- # Lenovo ThinkPad T480 OpenCore Configuation -->

![repository-open-graph-template-l24](https://github.com/user-attachments/assets/93d4fbc8-b233-4182-86d0-cc45ec1d32ae)


[![macOS](https://img.shields.io/badge/macOS-Big_Sur-red.svg)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Monterey-hotpink.svg)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Ventura-orange.svg)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Sonoma-brightgreen.svg)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Sequoia-lightblue.svg)](https://www.apple.com/macos/macos-sequoia/) 
[![OpenCore](https://img.shields.io/badge/OpenCore-1.0.1-blue)](https://github.com/acidanthera/OpenCorePkg)
[![License](https://img.shields.io/badge/license-MIT-purple)](/LICENSE)

<p align="center">
   <strong>Status: Maintained</strong>
   <br />
   <a href="https://github.com/tetenc555/Opencore-ThinkPad-T480/releases"><strong>Download now »</strong></a>
   <br />
   <a href="https://github.com/tetenc555/Opencore-ThinkPad-T480/issues">Report Bug</a>
   ·
   <a href="https://www.youtube.com/watch?v=thYDWyJuUq4">YouTube Video from Valnoxy</a>
  </p>
</p>
</br>

## ⚠️ Disclaimer
This guide is only for the Lenovo ThinkPad T480. I am NOT responsible for any harm you cause to your device. This guide is provided "as-is" and all steps taken are done at your own risk.

> [!IMPORTANT]
> I recommend switching to an Broadcom card. I will use a BCM94360NG and this EFI principal purpouse is to run the newer macOS with this card.

> The ACPI patches and the style of this README are from [EETagent](https://github.com/EETagent/T480-OpenCore-Hackintosh).

> This repository is forked from [MultimediaLucario](https://github.com/MultimediaLucario/Lenovo-ThinkPad-T480) and a bit tweaked here and there, please checkout his fork too.



&nbsp;

## 💻 Tested devices
Some users have reported that similar ThinkPads are compatible with this OpenCore configuration. Here is a list of these devices:

- Lenovo ThinkPad T580
- [Lenovo ThinkPad X280](https://github.com/valnoxy/t480-oc/discussions/47)

## Introduction

<details>
<summary><strong>💻 My Hardware</strong></summary>
<br>
These are the Hardware component I use. But this OpenCore configuation <strong>should still work</strong> with your device, even if the components are not equal.

Check the model of your WiFi & Bluetooth card. Intel cards should be compatible with itlwm (or AirportItlwm). If your card is from another manufacturer, please check if your card supports macOS. macOS Sonoma no longer supports Broadcom Wifi cards.

| Category  | Component                            |
| --------- | ------------------------------------ |
| CPU       | Intel Core i7-8650U                  |
| GPU       | Intel UHD Graphics 620 / NVIDIA GeForce MX150 (Disabled on macOS, works in Windows via BootCamp)|
| SSD       | LiteOn NVME SSD 512GB		   |
| Memory    | 16GB DDR4 2400Mhz                    |
| Camera    | Camera with Windows Hello Face Recognition (only the camera works on macOS, works in Windows via BootCamp)|
| WiFi & BT | Apple BCM94360NG NVME from AliExpress	 |
| Keyboard  | Backlight Keyboard |
| Display | 1080p panel with TouchScreen |

</details>  

</details>

<details>  
<summary><strong> 📸 Photos </strong></summary>
</br>

![LAPTOP](https://raw.githubusercontent.com/tetenc555/Opencore-ThinkPad-T480/refs/heads/main/assets/IMG_1624.HEIC)
![SETUP](https://github.com/tetenc555/Opencore-ThinkPad-T480/blob/main/assets/SETUP.JPG?raw=true)
![4K_60_HDMI](https://raw.githubusercontent.com/tetenc555/Opencore-ThinkPad-T480/refs/heads/main/assets/IMG_1619.HEIC)
![UNIVERSALCONTROL](https://raw.githubusercontent.com/tetenc555/Opencore-ThinkPad-T480/refs/heads/main/assets/IMG_1621.HEIC)
![BOOTCAMP](https://raw.githubusercontent.com/tetenc555/Opencore-ThinkPad-T480/refs/heads/main/assets/IMG_1622.HEIC)
![AIRDROP](https://github.com/tetenc555/Opencore-ThinkPad-T480/blob/main/assets/AIRDROP.PNG?raw=true)


</details>  

</details>


&nbsp;

## Installation

<details>  
<summary><strong> ⚠️ Anti-Piracy Warning / Disclaimer ⚠️ </strong></summary>
</br>
	
### ⚠️ PIRACY IS NO PARTY! ⚠️
I do not endorse or condone the use of pre-configured Hackintosh Distros because not only they cause unnecessary harm to your machine but it is considered to be a form of **Software Piracy**. Software Piracy is a serious crime according to copyright law and is punishable for up to 10 years in prison. 
</details>



<details>  
<summary><strong>📝 Requirements</strong></summary>
</br>

You must have the following items:
- Lenovo ThinkPad T480 (Obviously 😁).
- Access to a working Windows machine with Python installed.
- A pendrive with more than 4 GB (Remember that during the preparation we will format the flash drive to create the installation media).
- an Internet connection (recommended via Ethernet).
- 1-2 hours of your time.

</details>

<details>  
<summary><strong>⚙️ Preparation</strong></summary>
</br>

### Create the install media

First of all, you will need the install media of macOS. I will use [macrecovery](https://github.com/acidanthera/OpenCorePkg) to download and create the macOS Install media.

With macrecovery, the process is the following:
- Download [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) as a ZIP.
- Extract the OpenCorePkg-master.zip file.
- Open ```cmd.exe``` with Administrator privileges and change the directory to OpenCorePkg-master\Utilities\macrecovery.
- Enter the following command to download macOS:
```
# Monterey (12)
python macrecovery.py -b Mac-E43C1C25D4880AD6 -m 00000000000000000 download

# Ventura (13)
python macrecovery.py -b Mac-7BA5B2D9E42DDD94 download

# Sonoma (14)
python macrecovery.py -b Mac-CFF7D910A743CAAF -m 00000000000000000 download
```
- After the download succeeded, type ```diskpart``` and wait until you see ```DISKPART>```

- Plug-in your pendrive and type ```list disk``` to see your disk id.

- Select your pendrive by typing ```select disk <diskid>```

- Now we are gonna clean the pendrive and convert it to GPT. First, type ```clean``` and then ```convert gpt```.

>  **Note**: If an error occurred, try to convert again by typing ```convert gpt```.

- After the pendrive is clean and converted, we will create a new partition where we can put our files on. First, type ```create partition primary```, then select the new partition with ```select partition 1``` and format it ```format fs=fat32 quick```.

- Finally, mount your pendrive by typing ```assign```

- Now, close the Command Prompt and create the folder ```com.apple.recovery.boot``` on the pendrive. Copy ```OpenCorePkg-master\Utilities\macrecovery\BaseSystem.dmg``` and ```Basesystem.chunklist``` into that folder.

>  **Note**: If you can't find BaseSystem.dmg, use RecoveryImage.dmg and RecoveryImage.chunklist instead.

After the install media was created, we need to make the USB drive bootable.

### Updating Thunderbolt Firmware
To have thunderbolt fully working on macOS, you need to make sure you have FW23 (latest).

To do that, right click on Thunderbolt Control Center in system tray and, in the About section, check the FW. You should update cause Lenovo also [fixes a serious problem](https://www.notebookcheck.net/ThinkPad-Thunderbolt-3-failure-What-s-happening-why-it-s-happening-and-how-to-fix-it.451207.0.html) on this new FW. 

You can either do the update via Lenovo Vantage or following [these instructions](https://github.com/pierpaolodimarzo/ThinkPad-T480/issues/9)

<strong>Thanks pierpaolodimarzo for the help on making thunderbolt work on this machine! - Becca </strong>

### Configure and install OpenCore
Download the EFI folder from this repo, you will find the latest files under the release tab or just download the repo as it is. Move the folder to the root of your pendrive (e.g. J:\) and rename the folder to ```EFI```.

#### GenSMBIOS
We need a script, called [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS), to create fake serial number, UUID and MLB numbers. **This step is essential to have working iMessage, so do not skip it!**

The process is the following:

- Download GenSMBIOS as a ZIP, then extract it.
- Start GenSMBIOS.bat and use option ```1``` to download MacSerial.
- Choose option ```2```, to select the path of the config.plist file. It will be located in ```EFI -> OC``` folder.
- Choose option ```3```, and enter ```MacBookPro15,2``` as the machine type.
- Press ```Q``` to quit. Your config now should contain the requied serials.

#### Enter the proper ROM value
After adding serials to your config.plist, you have to add the computer's MAC address to the config.plist file. **This step is also essential to have a working iMessage, so do not skip it.** We need a Plist editior, to write the MAC address into the config.plist file. I used [ProperTree](https://github.com/corpnewt/ProperTree), since it works on Windows too. You have to change the MAC address value in the config.plist at

```PlatformInfo -> Generic -> ROM```

Delete the generic ```112233445566``` value, and enter your MAC address into the field, without any colons. Save the Plist file, and it is now ready to be written out to the EFI partition of your install media.

#### Default keyboard layout and language
The default keyboard layout and language is ```German```. To change the language, edit the value of ```NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82 -> prev-lang:kbd``` to the value of your language. If your value contains an underscore "```_```", replace it with a hyphen "```-```". The value for English would be ```en-US:0```. You can find a list of all language values [here](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt).

### Install OpenCore
After you've finished with the neccesary tweaks, you have to copy the EFI folder to the EFI partition of your pendrive.

</details>

<details>  
<summary><strong>🚚 Installation</strong></summary>
</br>

### Prepare BIOS
The bios must be properly configured prior to installing macOS.
In Security menu, set the following settings:

-  `Security > Security Chip`: **Enabled** did it for Windows 11 and it worked fine. You should disable if you're not using Windows.
-  `Memory Protection > Execution Prevention`: must be **Enabled**
-  `Virtualization > Intel Virtualization Technology`: must be **Enabled**
-  `Virtualization > Intel VT-d Feature`: must be **Enabled**
-  `Anti-Theft > Computrace -> Current Setting`: must be **Disabled**
-  `Secure Boot > Secure Boot`: must be **Disabled**
-  `Intel SGX -> Intel SGX Control`: must be **Disabled**
-  `Device Guard`: must be **Disabled**

In Startup menu, set the following options:

-  `UEFI/Legacy Boot`: **UEFI Only**
-  `CSM Support`: **No**

In USB menu, set the following options:
- `Always On USB`: **Disabled** - this is important! Enabling this breaks thunderbolt.

In Thunderbolt menu, set the following options:

-  `Thunderbolt BIOS Assist Mode`: **Disabled**
-  `Wake by Thunderbolt(TM) 3`: **Disabled**
-  `Security Level`: **Disabled**
-  `Support in Pre Boot Environment > Thunderbolt(TM) device`: **Enabled**


Now you can go through the install.

### Install macOS
1. Boot from USB, press ```SPACE``` and select the USB drive inside of OpenCore ```"NO NAME (DMG)" or similar```.
>  **Note:** The first boot may take up to 20 minutes.
2. Wait for the macOS Utilities screen.
3. Select Disk Utility, select your disk and click erase. Give a name and choose **APFS** with **GUID Partition Map**.
4. After erasing, go back and select **Reinstall macOS** and follow the steps on your screen. The installation make take up to **2 hours**.
>  **Note:** Your PC will restart multiple times. Just boot from USB and select your disk inside of OpenCore. (named macOS Installer or the disk name).
5. Once you see the `Region selection` screen, you are good to proceed.
6. Create your user account and everything else.

### Fixing Broadcom Wi-Fi (Required for Sonoma and Later! Older versions should work OOTB)
Everything is already configured on the EFI so we just need to run OCLP patch
1. Use an wired connection via Ethernet, Bluetooth or iPhone USB to download OCLP via their website
2. Run the Post-Installation Root Patch and reboot! 

Enjoy full continuity on your setup <3

</details>

<details>  
<summary><strong>♻️ Upgrade macOS / Switch EFI</strong></summary>
</br>

If you plan to upgrade your macOS (or updating the EFI / switching to HeliPort), you'll need a different OpenCore configuation (EFI). Please follow these steps:

> Note: Download the desired macOS version in the Settings before following these steps, if you are connected via WiFi.

1. Download the newest release & [ProperTree](https://github.com/corpnewt/ProperTree) and extract it.
2. Start ProperTree and load the ```Config.plist``` on your EFI partition. (File -> Open)
> Note: You can mount your EFI partition by pressing ```ALT + SPACE```, typing Terminal and enter the following command: ```sudo diskutil mountDisk disk0s1```.
3. Now also load the new configuration file from the repo for the desired macOS installation (or HeliPort config). 
4. You should now have 2 ProperTree-windows open on your screen.
5. Go in both windows to ```Root -> PlatformInfo -> Generic```. Transfer ```MLB, ROM, SystemProductName, SystemSerialNumber and SystemUUID``` to the new config. 
6. Save the new config (File -> Save) and close both windows.
7. Now delete your existing EFI folder from the EFI partition and copy the new one to it. (Make sure that the Directorys ```Boot and OC``` are in ```EFI```).

If you want to upgrade macOS, download the desired macOS version in the Settings app and perform the upgrade like on a real Mac.

</details>

&nbsp;

## Post-install (optional)

<details>  
<summary><strong>💾 Install OpenCore to Hard drive (RECOMMENDED!)</strong></summary>
</br>

1. Press `ALT + SPACE` and open terminal. Type `sudo diskutil mountDisk disk0s1` (where disk0s1 corresponds to the EFI partition of the main disk)
2. Open Finder and copy the EFI folder of your USB device to the main disk's EFI partition.
3. Unplug the USB device and reboot your laptop. Now you can boot macOS without your USB device.

</details>

<details>  
<summary><strong>✏️ Create a offline install media (Optional)</strong></summary>
</br>

In case of reinstalling macOS, a offline install media can save some time. You also don't need an Ethernet connection for the installation.
To create a offline install media, you need the following stuff: 

- macOS Installer from the App Store.
- A 16 GB pendrive (Keep in mind, during the preperation we will format the disk to create the install media).

Press `ALT + SPACE` and open Disk utility. Select your USB device and click erase. Name it `MyUSB` and choose **Mac OS Extended** with **GUID Partition Map**. After erasing the USB device, close Disk utility.

Now press `ALT + SPACE` and open terminal. Type the following command:

Big Sur:
```sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/MyUSB --downloadassets```

Monterey:
```sudo /Applications/Install\ macOS\ Monterey.app/Contents/Resources/createinstallmedia --volume /Volumes/MyUSB --downloadassets```

After creating the install media, copy your EFI folder to the EFI partition of your USB device.


</details>
<details>
<summary><strong>🖥️ Configure HIDPI for your monitors OwO (Optional)</strong></summary>
</br>

You can enable native HIDPI configurations with [this library](https://github.com/xzhih/one-key-hidpi)! I recommend doing it on your main display on any resolution, as i myself was using the full hd configuration on a hd screen on my old Lenovo Ideapad. This will cause some pixelation on these HD screens tho. For FullHD and 2K Built-Ins it is a super recommended configuration, cause you can get better screenshots and native scaling resolutions on system settings, as you can see right here:

<img src="https://github.com/tetenc555/Opencore-ThinkPad-T480/blob/main/assets/ScreenshotHIDPI.png" width="500px" height="auto" />

To do this, follow these steps:
1. Access the [repo](https://github.com/xzhih/one-key-hidpi) and download it as zip (or clone it) on any folder
2. Open terminal on the HIDPI-master folder
3. Run the command file (using ./)
4. Select your screen (if you have more than one), your resolution and the icon you preffer (for the built-in one, i recommend the macbook pro icon)
5. If you have problems with scaling after sleep, run it again and choose the resolution with "fix scale after sleep" option.


</details>
<details>
<summary><strong>💤 Configure your preffered sleep mode! ^.^</strong></summary>
</br>

By simply running the command "sudo pmset -a hibernatemode X" you can choose when your laptop will hibernate instead of sleeping! This can be useful for energy saving or quicker coming back to your work. Just change the X to the mode you like the most! All are supported (25 and 0 are fully tested, im still testing 3 but it should hibernate fine after some hours. Sleeping in 3 is working as it should.)

| Mode              | Details                    |
| ----------------- | -------------------------- |
| 0                 | Only sleep. Use this if you dont want hibernation.      | 
| 3                 | Sleeps normally, but after some hours (3 hours if <50% battery, else 24 hours), it hibernates to save battery (Recommended because it will probably save u to go to wake your laptop only for it to be dead)|
|25                 | Only hibernates. Better for maximum battery saving, as it completely shuts off the computer while youre not using it. It takes longer to wake up and to go to the hibernation state then from sleep. |


</details>

<details>
<summary><strong>😼 Use bootcamp for booting on Windows!</strong></summary>
</br>

Although you can simply enable bootpicker and always boot from there (or use the esc key to go to the picker), you can have a clean method of switching systems, using BootCamp. macOS version works out of the box, but Windows version has to be installed. To do this, you need to inject your smbios in Windows by:

- Disable CustomSMBIOSGuid in Kernel -> Quirks
- Change from Custom to Create in PlatformInfo -> UpdateSMBIOS

and then simple use [this tool](https://github.com/timsutton/brigadier) in Windows to download Boot Camp. After that, just install the setup file and the BootCamp icon should pop up on your taskbar, makig it possible to change the default setting of opencore without using the picker!


I recommend doing this procedure in this order, to mitigate any drivers problem and have Broadcom Wi-Fi and Bluetooth drivers also installed in the easiest way possible:
1. Activate Boot Picker on Misc -> Show Picker
2. Partitionate your SSD
3. Install Windows and drivers (Broadcom prob will not be installed and it should be the only one missing)
4. Restart to macOS and enable SMBIOS injection
5. Boot on Windows and download and install BootCamp via brigadier (Broadcom Drivers should now be installed)
6. Restart to macOS and disable SMBIOS injection

You can now also disable bootpicker! Remembering that even disabled, you can get into it by holding esc while powering on the laptop, so thats why this is my favorite setup.


</details>

&nbsp;

## Status

Remember to check [here](https://github.com/tetenc555/Opencore-ThinkPad-T480/issues) for more deitaled Issues that im trying to solve! 

<details>  
<summary><strong>✅ What's working :3 </strong></summary>
</br>
 
- [X] Intel WiFi & Bluetooth (Please configure it yourself or use [Multimida Lucario's EFI](https://github.com/MultimediaLucario/Lenovo-ThinkPad-T480))
- [X] Brightness / Volume Control
- [X] FullHD Screen with TouchScreens and Gestures (Gestures are trackpad-like)
- [X] Keyboard Backlight and Fan Control via YogaSMC
- [X] Battery Information
- [X] Audio (Audio Jack & Speaker)
- [X] USB Ports & Built-in Camera
- [X] Graphics Acceleration
- [X] 4k60 output via HDMI 2.0 (in HDMI Port)
- [X] Trackpoint / Touchpad
- [X] Power management / Sleep
- [X] Hibernation
- [X] FaceTime / iMessage (iServices)
- [X] HDMI
- [X] Automatic OS updates
- [X] Handoff / Universal Clipboard
- [X] Sidecar (Cable) / AirPlay to Mac
- [X] SIP / FireVault 2 (Using 03080000 configuration for Native Wi-Fi in Sequoia)
- [X] USB-C 3.1 with DisplayPort (4k60 not working via USB-C) (Check issue #9)
- [X] Thunderbolt 3
- [X] Dualbooting Windows (with OpenCore and BootCamp)

### <strong>With Broadcom Wifi:</strong>
- [X] AirDrop & Continuity (with Intel Wifi)
- [X] Sidecar Wireless (connecting works! Sidecar Wireless is currently broken.)

</details>

<details>  
<summary><strong>⚠️ What's not working =.= </strong></summary>
</br>

- [ ] 4k60 output via HDMI 2.0 (in both USB-Cs) (Check issue #9)

### <strong>Non-Fixable</strong>
- [ ] Safari DRM ```Use Chromium powered Browser or Firefox to watch Amazon Prime Video, Netflix, Disney+ and others```
- [ ] Fingerprint Reader (Disabled with NoTouchID kext)
- [ ] Facial Recognition (Camera works fine on macOS)

### <strong>Without Intel Wifi:</strong>
- [ ] AirDrop & Continuity (with Intel Wifi)
- [ ] Sidecar Wireless
- [ ] Apple Watch Unlock


</details>

<details>  
<summary><strong>🔄 Not tested (yet) :< </strong></summary>
</br>

If you tried some of these please let me know via the discussions tab!
- [ ] WWAN
- [ ] Dualbooting Linux (with OpenCore)
- [ ] HotPlugging ThunderBolt (USB-C Hotplugging is working!)

### <strong>With Broadcom Wifi:</strong>
- [ ] Apple Watch Unlock


</details>

&nbsp;


## 📜 License

This repo is licensed under the [MIT License](https://github.com/valnoxy/t480-oc/blob/main/LICENSE).

OpenCore is licensed under the [BSD 3-Clause License](https://github.com/acidanthera/OpenCorePkg/blob/master/LICENSE.txt).

<hr>
<h6 align="center">© 2018 - 2024 valnoxy. All Rights Reserved. 
<br>
By Jonas Günner &lt;jonas@exploitox.de&gt;</h6>
<p align="center">
	<a href="https://github.com/valnoxy/t480-oc/blob/main/LICENSE"><img src="https://img.shields.io/static/v1.svg?style=for-the-badge&label=License&message=MIT&logoColor=d9e0ee&colorA=363a4f&colorB=b7bdf8"/></a>
</p>
