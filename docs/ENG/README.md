# What I did when installing Hackintosh on Dell OptiPlex 3060 system unit

ENGLISH | [RUSSIAN](/README.md)

This instruction I wrote for myself that after reinstallation not to remember as how to do. The instructions are written after installing macOS Mojave 10.14.6. to the system unit  [DELL OptiPlex 3060](https://www.dell.com/support/home/product-support/product/optiplex-3060-desktop/).

## Dell OptiPlex 3060 system unit features

* Processor
  * Intel Core i5-8500 3.0GHz, Turboboost 4.1GHz, Coffee Lake
* Video card
  * Intel UHD Graphics 630
* RAM
  * 8 GB DDR4 2666MHz
* Motherboard
  * Dell OptiPlex 3060
* Sound adapter
  * Realtek ALC 255
* Bluetooth
  * ?
* Wifi
  * ?
* Ethernet
  * Realtek RTL8168/8111 PCI-E Gigabit Ethernet Adapter (PHY: Realtek RTL8111)

In the [OtherFiles](/OtherFiles) folder there is a system report from teh AIDA64 program, but the report is not complete, because Windows was launched from an external hard disk and it did not have time to download and install all the necessary drivers

## What worked and did not work to "revive"

### What works

* Intel UHD Graphics 630
* Intel Quick Sync graphics acceleration
* USB 3.0 and USB 2.0 ports
* 3.5 mini Jack port
* Ethernet

### What doesn't work

* 2 monitors simultaneously (one via HDMI, the other via DisplayPort). Only 1 of the connected devices works
* FaceTime, iMessage, HandOff, Continuity - in order to make these functions work you need wifi (and probably bluetooth, but it's not accurate). Maybe you need to buy compatible with macOS Mojave Wifi modules and replace or connect them, or you can make the existing Wifi and bluetooth modules work, but I did not want to do it, because I use the Internet via Ethernet wire

### What not verified

* Wifi
* Bluetooth
* Turboboot
* SpeedStep
* USB
* HDMI Audio
* Drive (it is recognized in macOS and can even be opened by pressing a couple of buttons in the interface, but I don't have a DVD/CD to check the drive)

## Pre-installation preparation

Just in case, save all important files on a separate flash drive or in the cloud.

Make a system report in AIDA64 and archive the EFI folder that you have on your flash drive, and upload to the cloud, so that in case of an emergency, you can correctly describe the situation by attaching files with a description and that you could help.

MacOSX can be installed on a disk (without formatting) only with GPT (GUID Partition Table) markup.

It is recommended that you erase (format) the entire disk during MacOSX installation, but this is not required.

If you have only 1 drive (1 HDD or 1 SSD) that already has Windows installed and you want to install MacOSX next to Windows, there are several solutions:

* During MacOSX installation, erase (format) the entire disk, but then all files will be deleted
* Buy a separate drive and install MacOSX on it
* If your drive is formatted GPT, it is possible in Windows to separate partition and then it to install MacOSX
  * Learn how to mark up can be in Windows, to do this, open the "disk Management" (click RMB on start), then open the properties of the disk (click RMB on the disk itself, and not on the partitions, where it says "Disk 0" or "Disk 1"), click the "Volumes" tab and there look at the partition style. If the partition style is "table with GUID partitions" then all is well
  * To separate or create a partition in WIndows, you can in the same program "disk Management", for this press the PCM on the partition from which you will separate another partition and in the konektnom menu press "Compress" and then choose how many megabytes to compress the selected partition. Accordingly, anything more than those megabytes will be formed in the new Unallocated region that you can mark up any file system, but FAT32 is better in. Then, during the installation of MacOSX, you need to select this partition in the Disk utility, format it in APFA or HFS+ (depending on the version of MacOSX you are installing) and select this partition when installing MacOSX
* If your disk is marked in MBR, you will need to convert it to GPT, or erase (format) it in Disk utility during MacOSX installation
  * Learn how to mark up can be in Windows, to do this, open the "disk Management" (click RMB on start), then open the properties of the disk (click RMB on the disk itself, and not on the partitions, where it says "Disk 0" or "Disk 1"), click the "Volumes" tab and there look at the partition style. If the partition style is "MBR", this is bad
  * To convert MBR to GPT on Windows without losing data, you need to use third-party programs. As far as I know, these programs "Paragon Hard Disk Manager", "AOMEI Partition Assistant" and "MiniTool Partition Wizard" and possibly some other utilities allow to convert markup from MBR to GPT without data loss. Unfortunately, only paid versions of these programs allow you to convert. Personally, I used "MiniTool Partition Wizard" and everything was converted without data loss. Also, after switching off, you need to switch the boot mode from CSM (Legacy) to UEFI in the BIOS/UEFI settings.

## BIOS / UEFI setup

These parameters are very important

* Reset to factory settings
* Enable UEFI mode
* Enable AHCI
* Disable Secure Boot
* Set VideoRAM 64 MB


## Create a bootable flash drive

1. [Download BootDiskUtility](http://cvad-mac.narod.ru/index/bootdiskutility_exe/0-5)
2. Download [special obraz](https://applelife.ru/threads/bdu-macos-i-clover-iz-windows-izgotovlenie-zagruzochnoj-flehshki.37189/page-57#post-557498) macOS Mojave 10.14.6 for BDU (this is the file with the extension .hfs, perhaps it will be in the archive)
3. Insert the flash drive size of 8 GB or more (in any port)
4. IN BDU

   * Open Options -> Configuration
   * Click "Check Now" and wait until the line is updated next
   * Everything else leave default
   * Click "OK"
   * Select the flash drive and press the "Format" button and confirm the action

     > When the flash drive is formatted it will create 2 sections: ESP and an empty section. The ESP will already have the Clover bootloader extracted from the ISO image from the repository on Sourceforge

   * Select the second section (you may need to click on the "+" to the left of the flash drive), it is usually at the bottom
   * Click "Restore" and select files 5.hfs
   * Wait for the progress bar of the image recording in the BDU to reach the end
   * Readily

There is also a guide with pictures in the pdf file. This mini manual is called "BDU_FAQ_STARCOM" and [attached to этому](https://applelife.ru/threads/bdu-macos-i-clover-iz-windows-izgotovlenie-zagruzochnoj-flehshki.37189/page-57#post-557498) message.

## Setting up a bootable flash drive

After creating a flash drive with the bootloader Clover and the MacOSX system itself, you need to configure the flash drive, or rather the bootloader, because just so MacOSX on a computer not from Apple will not be installed due to the lack of some differences in hardware between Apple computers and conventional PCs or laptops.

### Drivers to be used

[Drivers list](/docs/RUS/Configuring/InstalledDrivers.md)

### Setup the config file.plist

[Instructions for setting up the config file](/docs/RUS/Configuring/CustomizingConfig.md)

### Used kexts

[How to use kexts](/docs/RUS/Configuring/InstalledKexts.md)

## Install hackintosh macOS Mojave 10.14.6

Standard macosx installation:

1. If you are going to install MacOSX on a single Windows disk and the disk is partitioned into GPT, you need to separate the partition to install MacOSX, but if the dick is partitioned into MBR, then you need to convert it to GPT or buy a separate one to install MacOSX. Read more in the section "Preinstallation preparation"
2. If you do not need the files that are on the disk on which you will install MacOSX, then follow on
3. After setting up the boot stick, insert it into the computer, reboot and go to the BIOS/UEFI or a separate submenu. You need to choose to download from your flash drive and at the same time when you select the flash drive in the line with its full name, most likely, should be the word "UEFI"
4. Boot from a flash drive and get into the GUI boot loader menu Clover. After that, immediately press any arrows on the keyboard to reset the timer (this timer can be disabled in config.plist)
5. Switch arrow keys, select "Boot from the macOS Install ..."and press Enter
6. Wait until the window with the choice of language is loaded and choose the language
7. In the top panel (you need to move the cursor to the top of the screen) or in the window that appears, open the Disk utility
8. Click on the "View" button in the upper left corner of the window (or in the top panel) and switch the view to "Show all devices"
9. Choose your disk and press the "Erase"button. You can also partition the disk after you install MacOSX in Disk utility
   * Name: can be field any, but, perhaps, better English letters
   * Format: choose APFS
   * Scheme: GUID partition table 
10. Close the disk utility and choose "Install macOS"
11. Select the partition you created in the Disk utility. It will be installed on it. Click install
12. The process may not last as many minutes as indicated on the screen. Every few minutes, move the cursor so that the computer does not go to sleep
13. When the computer starts to reboot you need to start booting from your boot stick and in the Clover GUI menu you need to select "Boot macOS from ..."and press Enter (instead of three dots will be the name of the partition that you wrote in the Disk utility)
14. Then perform manipulations on the initial setup of your hackintosh computer and configure your MacOS account. It is desirable to enter everything in English. You can switch the layout (language) by pressing Ctrl+Space, or Alt+Space, or Win+Space, or change the mouse in the upper right corner of the window. All further settings can be changed at any time in the System settings, so do not be afraid to make a mistake

## Configure macOS

Below are the most important, in my opinion, items that need to be included on most Hackintosh after installing the system.

1. In the terminal, enter `sudo spctl --master-disable` to disable Gatekeeper and install applications not only from MacAppstore
2. Enable TRIM for SSD drives using the command in the `sudo trimforce enable`terminal
3. Flip the `MyKeyboardBundle ' file.bundle` in `/Library/Keyboard Layouts` and ' /System/Library/Keyboard Layouts` or make this file using the program Ukelele and [Hyde](https://www.youtube.com/watch?v=Ll6UGWGSSv8). Then go to "System settings", "Keyboard", "input Sources" and add a new layout and remove the Russian layout.
4. [Install Clover](https://sourceforge.net/projects/cloverefiboot/) and configure it before installation (on the left of one of the steps will be the "configure" button")
   - Be sure to check the first two items - "Install only for UEFI" and "Install on ESP"
   - If Clover on your flash drive is configured, the remaining checkboxes can not be changed, and if Clover on the flash drive is not configured, then you can configure it in this menu
   - Mount the EFI partition of your disk and flash drive if they are not mounted
   - All files and folders with EFI stick copy to the EFI disk with the replacement and reboot

The complete list of settings that I use are described in the corresponding file [**configuring Mac OS x**](/docs/RUS/Configuring/ConfiguringMacOSX.md)

### Windows setup

[Description of the nuances of installing Windows next to Hackintosh](/docs/RUS/AboutWindows/InstallWindows.md)

### Windows settings

As a setting for Windows 10 to work with macOS, I needed to set up time synchronization and for convenience to make a partition for files with the ExFat file system. About ExFat section under the files I wrote above in the instructions for installing Windows.

About the time synchronization, you can read and download direct guide there:

* https://appstudio.org/faq/3068.html
* https://www.tonymacx86.com/threads/fix-incorrect-time-in-windows-osx-dual-boot.133719/

## Software installation

### Essential programs

If you have a hackintosh, not a real Apple computer, I recommend that these programs are always installed on your system. These programs are included in the list of Hackintosh Tools, but they are the most necessary.

1. Clover Bootloader https://sourceforge.net/projects/cloverefiboot/
2. CloverConfigurator https://mackie100projects.altervista.org/download-clover-configurator/
3. Plist Edit Pro https://www.fatcatsoftware.com/plisteditpro/

### Hackintosh programs

These programs are mainly used to configure Hackintosh, as a working MacOS tool, they are unlikely to be useful to you. Some of these programs, it is desirable to leave in your hackintosh in case something goes wrong and the system starts to "show off", because not everyone can determine how well and how fully configured your hackintosh.

[Hackintosh tools](/docs/RUS/ProgramsList/HackintoshTools.md)

### Framework programs for other programs

These programs are needed to run other programs or scripts. This is mainly used by different developers. If you need them, you will know what program you need without this list.

[Other Software](/docs/RUS/ProgramsList/OtherSoftware.md)

### Installed BY

Most of the programs from this list I use in my daily work. Naturally, the list is not the most complete, see and decide on your needs.

[Regular Software](/docs/RUS/ProgramsList/RegularSoftware.md)

## Benchmark testing

The list of tests, their description and results are presented in a separate file.

[Benchmark test results](/docs/RUS/BenchmarksTesting/benchmark_testing.md)

## More

### Wallpaper

You can find wonderful Wallpapers on the website https://unsplash.com/

### Threads on the forums

In these topics, I have published information about setting up and installing hackintosh for this system unit
