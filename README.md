# EXO Wings Linux
This repo documents the progress of installing and configuring Linux to run on the EXO Wings w1125 2in1

## Booting a Linux installer
The EXO w1125 uses a mixed architecture UEFI structure, where the CPU runs on 64bit mode, but the UEFI is 32bit only.

This means that not every Linux ISO will boot on this machine. In particular, you will need a Linux distro which ships `bootia32.efi` by default, or you will need to modify an existing ISO to include it ([Linuxium](https://linuxiumcomau.blogspot.com/search/label/ISOs) offers Ubuntu ISOs modified to include `bootia32.efi` if you want to go that route).

In my case, i decided to install ArchLinux on my machine.

While this device does have a microSD card reader built-in, it doesn't like to boot from it, so you will need to plug your install medium to the USB port included in the machine's detachable keyboard

Note: i haven't managed to succesfully boot any ISO which includes `bootia32.efi` from a Ventoy USB on this machine. I recommend you burn the ISO directly to the install medium.

## Choosing a Desktop Enviroment
I chose to run Plasma Mobile for this device, but GNOME, KDE Plasma, and Phosh are good options too.

## Installing and Configuring Linux
### Initial Installation
I installed Arch using `archinstall`, choosing to NOT install a DE. The removable keyboard uses `es` keyboard distribution.

### Plasma Mobile Install
I installed Plasma Mobile by running `yay -S plasma-mobile konsole sddm` (this WILL take a while to compile, this machine isn't very fast).

Place `virtualkbd.conf` on `/etc/sddm.conf.d/` to get the virtual keyboard working, so that login on tablet mode is possible. 

### Screen Rotation Fix
By default, the screen rotation is reversed on this machine (rotating the device clockwise will rotate the screen counter-clockwise and viceversa). Fixing this requires placing the `61-sensor-local.hwdb` file on `/etc/udev/hwdb.d/` and running `systemd-hwdb update` and then `udevadm trigger` to apply the changes.

### Front and Back Cameras
Don't work yet :(
