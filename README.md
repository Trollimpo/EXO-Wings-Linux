# EXO Wings Linux
This repo documents the progress of installing and configuring Linux to run on the EXO Wings w1125 2in1

## Booting a Linux installer
The EXO w1125 uses a mixed architecture UEFI structure, where the CPU runs on 64bit mode, but the UEFI is 32bit only.

This means that not every Linux ISO will boot on this machine. In particular, you will need a Linux distro which ships `bootia32.efi` by default, or you will need to modify an existing ISO to include it ([Linuxium](https://linuxiumcomau.blogspot.com/search/label/ISOs) offers Ubuntu ISOs modified to include `bootia32.efi` if you want to go that route).

In my case, i decided to install ArchLinux on my machine.

While this device does have a microSD card reader built-in, it doesn't like to boot from it, so you will need to plug your install medium to the USB port included in the machine's detachable keyboard

Note: i haven't managed to succesfully boot any ISO which includes `bootia32.efi` from a Ventoy USB on this machine. I recommend you burn the ISO directly to the install medium.

# Choosing a Desktop Enviroment
I chose to run Plasma Mobile for this device, but GNOME, KDE Plasma, and Phosh are good options too.

# Installing and Configuring Linux
## Initial Installation
I installed Arch using `archinstall`, choosing to NOT install a DE. The removable keyboard uses `es` keyboard distribution.

## AUR Helper
`sudo pacman -Syu`

`sudo pacman -S --needed base-devel git`

`git clone https://aur.archlinux.org/yay.git`

`cd yay`

`makepkg -si`

## Plasma Mobile Install
### Install Plasma Mobile

`yay -S plasma-mobile konsole sddm dolphin` (this WILL take a while to compile, this machine isn't very fast).

### Enable network manager and bluetooth

`systemctl enable NetworkManager.service`

`systemctl enable bluetooth.service`

### Install Bluetooth manager

`yay -S bluedevil`

### Virtual keyboard on login screen

Run `yay -S maliit-keyboard qt5-wayland`

Place `virtualkbd.conf` on `/etc/sddm.conf.d/` 

## Screen Rotation Fix
By default, the screen rotation is reversed on this machine (rotating the device clockwise will rotate the screen counter-clockwise and viceversa).

Fixing this requires installing `iio-sensor-proxy` and placing the `61-sensor-local.hwdb` file on `/etc/udev/hwdb.d/`

Run `systemd-hwdb update` and `udevadm trigger`; then reboot to apply changes. 

## Front and Back Cameras
Don't work yet :(

## TPM 90s Startjob Fix
`systemctl mask dev-tpmrm0.device`
