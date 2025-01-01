# EXO Wings Linux
This repo documents the progress of installing and configuring Linux to run on the EXO Wings w1125 2in1

## Booting a Linux installer
The EXO w1125 uses a mixed architecture UEFI structure, where the CPU runs on 64bit mode, but the UEFI is 32bit only.

This means that not every Linux ISO will boot on this machine. In particular, you will need a Linux distro which ships `bootia32.efi` by default, or you will need to modify an existing ISO to include it ([Linuxium](https://linuxiumcomau.blogspot.com/search/label/ISOs) offers Ubuntu ISOs modified to include `bootia32.efi` if you want to go that route).

In my case, i decided to install ArchLinux on my machine.

Note: i haven't managed to succesfully boot any ISO which includes `bootia32.efi` from a Ventoy USB. I recommend you burn the ISO directly to the install medium.

While this device does have a microSD card reader built-in, it doesn't like to boot from it, so you will need to plug your install medium to the USB port included in the machine's detachable keyboard

