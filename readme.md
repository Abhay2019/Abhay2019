### mac OS USB Driver

## Prepare

* Disable System Integrity Protection.
    * From the Apple menu select Restart.
    * As your Mac restarts, press and hold down the Command(?) + R keys immediately upon hearing the startup chime. Hold the keys until the Apple logo appears to get the computer in Recovery mode.
The computer is now in Recovery mode. 
    * From the Apple menu select Utilities -> Terminal
    * Run the command: csrutil disable
    * From the Apple menu, select Restart.
 
## Run
* copy pacific.kext with sudo `sudo cp -R pacific.kext /tmp`.
* load module `sudo kextload /tmp/pacific.kext`
* plug USB Dongle
* check driver is presented `sudo kextstat | grep aq`
* wait for few seconds to up link.

## Stop
* perform `sudo kextstat | grep aq`. Possible output:

`146    0 0xffffff7f835b7000 0x9000     0x9000     com.aquantia.driver.usb.pacific (0) 5774CA9A-025B-36DB-899D-DA74905E40F5 <82 22 15 5 4 3 1>`.
* use module name from output `sudo kextunload -b com.aquantia.driver.usb.pacific`

## Install
* copy pacific.kext: `sudo cp -R pacific.kext /System/Library/Extensions`
* plug USB Dongle (at this case manual driver insertion is not needed)

## Uninstall
* Stop driver (see previous section)
* remove driver file from /System/Library/Extensions: `sudo rm -r /System/Library/Extensions/pacific.kext`