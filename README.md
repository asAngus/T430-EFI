# T430-EFI
Hackintosh High Sierra for Lenovo Thinkpad T430 <br />
Using Intel HD 4000 Graphics on i7-3520m, 250gb SSD, 1600x900 Screen <br />
Works: (sleep, volume, fn+brightness keys, iMessage, Camera) <br />
Doesn't Work: Integrated Microphone <br />
USB wifi required, install necessary drivers for your USB <br />

# USB Preparation (8 GB+)
- Open disk utility, select USB <br />
- Erase, Select MacOS Extended Journaled, GUID partition <br />
![Disk Utility](/README_Images/disk_util.png)
- Download High Sierra Installer, Through App Store or DosDude1's High Sierra Patcher (Sometimes store will download a useless 29 mb installer) <br />
- Open Terminal: sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --nointeraction --volume /Volumes/[YOUR USB] <br />
![Terminal](/README_Images/Term.png)
# Clover Custom Install Options
![Clover Select](/README_Images/Clover_select.png)
- MAKE SURE TO SELECT YOUR USB WHEN SELECTING LOCATION <br />

- Install Clover in the ESP <br />
- Boot Sectors <br />
    -> Install Boot0af in MBR
- Clover for BIOS (legacy) booting <br />
    -> Clover EFI 64-bits SATA
- BIOS Drivers, 64 bit <br />
    -> FSInject-64 <br />
    -> SMCHelper-64 <br />
    -> XhciDxe-64 <br />
    -> ApfsDriverLoader-64 <br />
- UEFI Drivers <br />
  -> EmuVariableUefi-64 <br />
	-> OsxFatBinaryDrv-64 <br />
- Install RC scripts on target volume
![Clover End](/README_Images/Clover_end.png)

# Insert EFI folder
Once Finished, there should be an EFI partition on your desktop <br />
If not: <br />
- diskutil list <br />
Find EFI for your usb <br />
- sudo diskutil mount /dev/diskXsX <br />
EFI will be in Finder or on Desktop <br />

If/When there is:<br />
- Move **contents** of EFI folder (from this repo in EFI.zip) into this partition <br />

# Install through USB
- Plug in USB, Boot T430, hit F12 on startup <br />
- In boot menu, boot from your USB <br />
- In Clover, navigate with arrow keys to the Options, hit enter on boot options, type -v, hit enter again, return <br />
- Boot the USB <br />
- Once prompted, open disk utility, format drive as APFS w/ GUID if using an SSD, macOS Extended Journaled w/ GUID if using a HDD <br />
- Takes a while, once done, close with the red button, install MacOS to your target drive <br />
- Once done, screen will probably go black & reboot 3/4 through installer, its done installing <br />
- Boot the USB, in clover, select your target drive <br />

# Install Clover on Your Target Drive
- This is so you no longer need to boot with USB <br />
- Get clover installer pkg onto your computer, I did this through USB or ethernet <br />
- Install with the same options as the USB, this time to our target drive <br />
- Follow "Insert EFI folder" but with the target drive instead of the USB <br />
