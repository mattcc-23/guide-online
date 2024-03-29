---
title: Guide
author: supernova
pubDatetime: 2023-09-03
postSlug: ""
featured: true
draft: false
tags:
  - guide
  - bootloader-unlock
  - fastboot-unlock
  - custom-rom
ogImage: "@assets/images/cover.png"
description: Complete guide for Realme 8 4G RMX3085 with unlocking boot loader and fastboot, installing custom roms and rooting
canonicalURL: https://guide.driedpampas.ro.eu.org/guide
---

# Realme 8 MEGAGUIDE

==================

> If you have any questions at any moment feel free to message [Realme 8 AOSP](https://t.me/Realme8AOSPGroup) on Telegram or [open a new Discussion](https://github.com/driedpampas/realme-8-megaguide/discussions/new/choose) on GitHub. Also check the [FAQ (frequently asked questions)](posts/FAQ/)

> Disclaimer - We WON'T be responsible if anything happens with your device. - Neither Windows 7 (old python version) nor RealmeUI 4 (lk method was patched) are supported

> ℹ️ If you have unlocked already skip to [[EXTRA] Installing a Custom recovery and ROM](#iii-installing--a-custom-recovery-and-rom)

> Make sure to back up your data, because you will lose it. If you want to back up your RealmeUI install just in case use the [Backup guide (in wiki)](posts/back-up-your-data)

> **✴️ Make sure to read and do all of the steps to avoid your device being bricked.**

> **📛 WARNING: RUI4 disables fastboot access if previously unlocked, only upgrade to RUI3 until it is resolved.**

> **✨✨✨ You can revert all the changes by following [Revert](posts/revert)**

---

## Table of Contents

---

# 0. Back up your system partitions

### Just in case something fails or your device gets bricked please use the [Backup guide (in wiki)](posts/back-up-your-data)

# I. Unlocking

## Prerequisites

- [Mediatek USB](https://drive.google.com/file/d/1UExJQxI1DmBGeDoYPul5YTXitOnsU6zx/view?usp=sharing)
- [USBDk](https://github.com/daynix/UsbDk/releases/download/v1.00-22/UsbDk_1.0.22_x64.msi)
- [Python from Microsoft Store](https://apps.microsoft.com/store/detail/python-310/9PJPW5LDXLZ5)
- [MTK Client archive](https://github.com/bkerler/mtkclient/archive/refs/heads/main.zip)
- [SP Flash tool](https://drive.google.com/file/d/11XeUnCYtARZg2kx7J2JWWeLULieSIYrx/view?usp=sharing)
- [A.19 RUI2 Firmware](https://drive.google.com/file/d/1Iy2hwZ0mHQtpHgpyRDRHMZv13FTTvups/view?usp=share_link)
- [C.18 RUI3 Firmware](https://drive.google.com/file/d/1YHSIr4itg_5dPE2IbWAH9N8g6L5CGmaG/view?usp=drive_link)

## 1. Installing prerequisites

1. ### Mediatek USB

   1. **Extract** and enter the folder of [Mediatek USB](https://drive.google.com/file/d/1UExJQxI1DmBGeDoYPul5YTXitOnsU6zx/view?usp=sharing) driver.
   2. Find the **.inf** file, right click and press install

      ![Image](https://i.imgur.com/niVRaOn.png)

2. ### Install [USBDk](https://github.com/daynix/UsbDk/releases/)

3. ### Install [Python from Microsoft Store](https://apps.microsoft.com/store/detail/python-310/9PJPW5LDXLZ5)

> **🛑 Do not disconnect the phone during the flashing and unlocking processes**

## 2. Downgrade to RUI2

1. **Extract** [MTK Client](https://github.com/bkerler/mtkclient/archive/refs/heads/main.zip) and open a cmd in the folder where you extracted the files

   ![Image](https://i.imgur.com/RJtobaI.png)

2. Get the needed libraries using command `python -m pip install -r requirements.txt`. Send the payload with `python mtk payload`. It should look like this:

   ![Image](https://i.imgur.com/WSQsVj1.png)

3. Make sure your phone is powered off, hold down both **Vol+, Vol-** and connect the usb cable. MTK Client should output something like this:

   ![Image](https://i.imgur.com/lr7HIN0.png)

4. The phone is now in BROM mode. Run the [SP Flash tool](https://drive.google.com/file/d/11XeUnCYtARZg2kx7J2JWWeLULieSIYrx/view?usp=sharing) `flash_tool.exe`

5. Click on `Options > Option...` and make sure the right **COM** **Port** is selected, UART enabled and baud rate is set to **921600**.

   ![Image](https://i.imgur.com/hnMsyeN.png)

6. Unpack [Haadi's A.19 RUI2 Firmware](https://drive.google.com/file/d/1Iy2hwZ0mHQtpHgpyRDRHMZv13FTTvups/view?usp=share_link) and load the `scatter.txt` file

   ![Image](https://i.imgur.com/VTwpXzC.png)

   > **🛑 Remember to uncheck: `opporeserve2` and `cdt_engineering`**

   | opporeserve2 (Signed partition)      | cdt_engineering (Digital warranty codes) |
   | :----------------------------------- | :--------------------------------------- |
   | ![](https://i.imgur.com/9Kp65P7.png) | ![](https://i.imgur.com/S6XOitJ.png)     |

7. Remember to have `Download Only` mode.

   ![Image](https://i.imgur.com/M3aUNBs.png)

8. Avoid moving your phone so as to not disconnect anything. This process will take up to 15-20 minutes. To get A.19 on your phone, click `Download`. [**No progress? Click me**](posts/FAQ/#1-why-is-there-no-progress-when-using-spflash-tool)

   ![Image](https://i.imgur.com/uSXflCJ.png)

9. If everything goes well, it should look like this.

   ![Image](https://i.imgur.com/qeJWt3a.png)

10. Before doing anything, we'll **WIPE the phone for safety.** Hold down **Vol-, and power button**, In recovery select wipe data, and then select **Format Data**.

## 3. Unlocking the bootloader

1. Open the console in [MTK Client's](https://github.com/bkerler/mtkclient/archive/refs/heads/main.zip) folder
2. Reboot your device, turn it off and Hold down both **Vol+, Vol-** - **(Don't leave the buttons until the command is done)**
3. Type `python mtk e metadata,userdata,md_udc` - This assetscommand wipes your data. It should look like this:

   ![](https://i.imgur.com/HfPsrpU.png)

4. Unlock the bootloader using command `python mtk da seccfg unlock`, the output should look like this

   ![](https://i.imgur.com/Su8RtHk.png)

   > **🔄 After this, turn on your phone. First boot will take around 5-20 minutes.**

   > **📛 You will see `dm-verity corruption` and `orange state` warnings. Press the _Power Button_ to continue. These are normal and will be patched later in the guide.**

5. Your bootloader is now unlocked.

> ❗ Check [FAQ (frequently asked questions)](posts/FAQ) if something does not work or you have questions

## 4. Upgrade to RealmeUI 3

1. Open a cmd again in [MTK Client's](https://github.com/bkerler/mtkclient/archive/refs/heads/main.zip) folder

   ![](https://i.imgur.com/RJtobaI.png)

2. Send the payload with `python mtk payload`:

   ![](https://i.imgur.com/WSQsVj1.png)

3. Make sure your phone is powered off, hold down both **Vol+, Vol-** and connect the usb cable. MTK Client should output something like this:

   ![Image](https://i.imgur.com/lr7HIN0.png)

4. The phone is now in BROM mode. Run the [SP Flash tool](https://drive.google.com/file/d/11XeUnCYtARZg2kx7J2JWWeLULieSIYrx/view?usp=sharing) `flash_tool.exe`

5. Click on `Options > Option...` and make sure the right **COM** **Port** is selected, UART enabled and baud rate is set to **921600**.

   ![](https://i.imgur.com/hnMsyeN.png)

6. Unpack [SG's C.18 RUI3 Firmware](https://drive.google.com/file/d/1YHSIr4itg_5dPE2IbWAH9N8g6L5CGmaG/view?usp=drive_link) and load the `MT6785_Android_scatter.txt` file

   ![](https://i.imgur.com/8APQvkx.png)

7. Remember to have `Download Only` mode

   ![](https://i.imgur.com/M3aUNBs.png)

8. Place your phone on a stable surface, to not disconnect anything. This process will take up to 15-20 minutes. To get C.18 on your phone, click `Download`. [**No progress? Click me**](posts/FAQ/#1-why-is-there-no-progress-when-using-spflash-tool)

   ![](https://i.imgur.com/uSXflCJ.png)

9. If everything goes well, it should look like this:

   ![Image](https://i.imgur.com/qeJWt3a.png)

10. Before continuing, you'll need to **WIPE the phone for safety.** Hold down **Vol-, and power button**, In recovery select wipe data, and then select **Format Data**.

![](https://i.imgur.com/08VdiB8.png)

> ❗ Check [FAQ (frequently asked questions)](posts/FAQ) if something does not work or you have questions

---

# II. Patching `lk`- qetting fastboot access and removing dm-verity and orange state warnings

> ❕ SKIP ONLY IF you unlocked with DEEP TESTING

> 🛑 Do not disconnect the phone during the process

1. Open the console again in `MTK Client` folder

   ![](https://i.imgur.com/RJtobaI.png)

2. Make sure your phone is powered off, hold down both **Vol+, Vol-** and connect the usb cable.

3. Run the command `python mtk r lk lk.bin`. There will now be a `lk.bin` file in **MTK Client** folder.

   ![](https://i.imgur.com/gL4Qpc2.png)

4. Go to this [website](https://lkpatcher.r0rt1z2.com/). Upload your lk.bin file and the `lk-patched.bin` will be downloaded. Move it to `MTK Client` folder. If the website gives an error check [FAQ #2](/posts/patching-lk-locally)

   ![](https://i.imgur.com/HOve3Mv.png)

5. Run command `python mtk w lk lk-patched.bin`

> Check [the FAQ](posts/FAQ/#2-i-patched-my-lk-but-the-phone-still-says-fastboot_verify_fail) if you have any issues

# III. Installing a Custom Recovery and ROM

## Prerequisites

- [latest platform-tools](https://dl.google.com/android/repository/platform-tools-latest-windows.zip) - you will get errors if you use old platform-tools
- [QcomMtk-Driver](https://www.mediafire.com/file/nninaiiqy1e5csa/New+QcomMtk_Driver_Setup_V2.0.1.1_GsmMafia.Com.exe) - driver
- ❗️ If you get an error: `fastboot: usage: unknown reboot target recovery` try this adb installer [ADB and Fastboot ++](https://github.com/K3V1991/ADB-and-FastbootPlusPlus/releases/download/v1.0.8/ADB-and-Fastboot++_v1.0.8.exe)
- only flash once (you should not need to reflash it) - [vbmeta image](https://github.com/bengris32/releases/releases/download/arrow-1.1/vbmeta.img) - vbmeta.img file
- a custom rom package - check out the [telegram group](https://t.me/Realme8AOSP) for ROMs
- GAPPS package - recommended [MindTheGApps for Android 13](https://androidfilehost.com/?fid=4279422670115734716)
- example recovery images:
  - 🎉 We now have [OrangeFox recovery](https://fcloud.howwof.pl/s/RBmEeMRZyDam8fZ) 🎉 - technically compatible with any rom
  - [lineage-os recovery](https://github.com/bengris32/releases/releases/download/3.0/lineage-20.0-20230613-UNOFFICIAL-nashc-recovery.img) - compatible with Pixel Experience and Lineage OS (and others, check the Custom ROM's description)
  - [leaf-os recovery](https://github.com/HowWof/releases/releases/download/leaf-2.0.1/recovery.img) - use ONLY with Leaf OS 2

## 1. Rebooting to fastboot

### Your device needs to be turned on

1. Open a command prompt window in the **platform-tools** folder.
2. **On your phone**, enable Developer Options and enable USB Debugging.
3. In the platform-tools folder open a command prompt and run `adb devices`. You will see `Allow USB Debugging for ...` on phone, check `Always allow...` and hit `Allow`.
4. In the command prompt run `adb reboot boootloader`. Phone will reboot to a screen that says `fastboot_unlock_verify ok`.

> ❗ Check [FAQ (frequently asked questions)](posts/FAQ) if something does not work or you have questions

## 2. Installing custom recovery and sideloading custom rom

> ⚠️ If switching between custom roms skip step 2.

> ⚠️ If the required recovery has not changed you may skip step 3 as well, and run `adb reboot recovery` directly.

1. Move the `recovery.img` and `vbmeta.img` files to the **platform-tools** folder.
2. Run the command `fastboot --disable-verity --disable-verification flash vbmeta vbmeta.img`. It should show

   ![](https://i.imgur.com/MZZyTBc.png)

3. Run the command `fastboot flash recovery recovery.img`. The phone should show `USB Transmission ok`/

   ![](https://i.imgur.com/t7wYi3R.png)

4. Now, reboot to recovery mode with the command `fastboot reboot recovery`

   ![](https://i.imgur.com/1zwXUmj.png)

5. In recovery, go to `Factory reset > Format data/factory reset > Format data`. **After** factory reset go back and select `Apply update > Apply from ADB`. You should see this when running `adb devices`:

   ![](https://i.imgur.com/MoiIS9k.png)

6. Now run the command `adb sideload custom-rom.zip` (replace _custom-rom.zip_ with custom rom package name). For example I flashed LeafOS 2:

   ![](https://i.imgur.com/QZqi1e1.png)

7. **ONLY** do this step on custom roms **WIHTOUT GAPPS / GMS** (check the rom's description to check). Select `Apply update > Apply from ADB` again and run `adb sideload gapps.zip` (replace _gapps.zip_ with package name).

   ![](https://i.imgur.com/DUEMXrn.png)

8. Once finished, in the recovery go back to `Reboot system now`. The phone will reboot into your Custom ROM.

> ⚠️ If you get a "Signature verification error" on your phone, click `Yes` to continue anyways, this goes the same to any other ZIPs you flash.

# IV. Rooting

![](https://i.imgur.com/tm2MVru.png)

## 1. With Magisk

### You will need

- [MTK Client](https://github.com/bkerler/mtkclient/archive/refs/heads/main.zip) - donwload on your pc
- [Magisk Manager (apk file)](https://drive.google.com/file/d/1LsHqdNqO7zOR2vhtxVCzC-JHiCN_l3gM/view?usp=drive_link) - download on your phone
- [latest platform-tools](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)

1. Open the console in [MTK Client's](https://github.com/bkerler/mtkclient/archive/refs/heads/main.zip) folder
2. Run `python mtk r boot boot.img`. Turn your device off, hold down both **Vol+, Vol-** and connect the device to the computer.

3. A `boot.img` file will be created in the folder. Turn your device on and copy the file to it.

4. Navigate to where you donwnloaded the Magisk Manager apk file and install it.

5. Open Magisk Manager and click install next to `Magisk`.

   ![](https://i.imgur.com/CAbHxPv.png)

6. Select `Patch vbmeta in boot image` and click `Select and patch a file`. The file picker will open, Find and select the `boot.img` you extracted.

   ![](https://i.imgur.com/d3QC6S8.png)
   ![](https://i.imgur.com/4m7CJfB.png)

7. When you see this screen, the patching is done and you will be givne the path of the patched `.img file`. Copy that file to your computer in the `platform-tools` folder.

   ![](https://i.imgur.com/D9qyjbG.png)

8. Connect your pphone to your computer, enable usb debugging on your phone and, in the `platform-tools` folder open a Command Prompt and run the command `adb devices`. Accept USB Debugging on your phone and run `and reboot bootloader`. The phone will reboot to a `fastboot_unlock_verify ok` screen.

9. Now in the cmd run the command `fastboot flash boot <>` and hit Enter. Once successfully transferred, run `fastboot reboot`

10. The phone will restart and you are now rooted with Magisk! ### To remove Magisk root, select `Uninstall > Complete uninstall` in the Magisk Manager app.

## 2. With KernelSU

> 🚫 ONLY WORKS ON CUSTOM ROMS (DO NOT ATTEMPT on RealmeUI)

### You will need

- [KernelSU zip file](https://drive.google.com/file/d/1hBYm9nA2EyCC-ioQruj5vNmrAlW1Ayta/view?usp=sharing) - download on pc
- [KernelSU manager (apk file)](https://github.com/tiann/KernelSU/releases/download/v0.6.7/KernelSU_v0.6.7_11210-release.apk) - Download this on your phone.

> ⚠️ If you get a "Signature verification error" on your phone, click `Yes` to continue anyways, this goes the same to any other ZIPs you flash.

1. ### You need to be in recovery mode; run `adb reboot recovery`
2. In recovery select `Apply update > Apply from ADB` and run `adb sideload kernelsu.zip`.

3. When completed tap `Reboot system now`. Your phone will restart. Navigate to where you donwnloaded the KernelSu Manager apk file and install it.

4. The app should show like this indicating thaat everything has been done correctly:

   ![](https://i.imgur.com/XhOFSXP.png)

5. If you want to remove KernelSU root, extract the `custom-rom.zip` you downloaded to flash the ROM, find and move the `boot.img` to the folder where adb is and run these commands in a command prompt:

- `adb reboot bootloader`
- `fastboot flash boot boot.img`

> 🎴 More extras in [WIKI](/tags/wiki)

# Special thanks & credits

> [Ben](https://github.com/bengris32/android_kernel_realme_mt6785) - Made everything possible by making the kernel for Realme 8  
> [bkerler](https://twitter.com/viperbjk) - developer of [MtkClient](https://github.com/bkerler/mtkclient)  
> [Roger](https://t.me/R0rt1z2) - creator of [oplus-unlock](https://github.com/R0rt1z2/oplus-unlock)  
> [Haadi](https://t.me/Haadi786H) - RUI2 firmware  
> [SGtriangle](https://t.me/SGtriangle) - RUI3 firmware  
> [HowWof](https://t.me/HowWof) - A lot of help, Leaf OS 2 for RMX3085 developer  
> [Ripper_Hybrid](https://t.me/Ripper_Hybrid) - provided KSU zip file, helped with wiki guides  
> [MrPotato6](https://t.me/MrPotato6) - Info and screenshots for Magisk rooting  
> [Nand kumar](https://forum.xda-developers.com/m/nand-kumar.8476267/) - original poster of backup guide  
> [Zako Chan](https://t.me/zakolakov106/) - Information about walkthrough with downgrade  
> [Tony stark](https://forum.xda-developers.com/m/tony-stark.7582728/) - [RUI2 unlock guide](https://forum.xda-developers.com/t/guide-realme-8-unofficial-new-method-unlock-bootloader-flash-twrp-and-root-rmx3085.4386473/)  
> [Original Custom ROM Guide](https://telegra.ph/Flash-LineageOS-on-Realme-8-06-05)  
> [Magisk & Developers](https://github.com/topjohnwu/Magisk)  
> [KernelSU & Developers](https://github.com/tiann/KernelSU)  
> Banner and others via [Canva](https://canva.com) - Refer to [Canva's CLA](https://www.canva.com/policies/content-license-agreement/) for more info  
> Text images made in [Drawing](https://maoschanz.github.io/drawing)  
> Telegram: [Realme 8 AOSP](https://t.me/Realme8AOSPGroup) Witten by [me](https://t.me/driedpampas) with 🫶.

> No guarantees are given at any point. Use with caution. Neither me nor contributors are responsible for any damage you do to your device(s).
