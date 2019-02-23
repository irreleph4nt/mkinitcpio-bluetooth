# mkinitcpio-bluetooth
mkinitcpio hook to enable bluetooth connectivity during boot.

# Instructions
This hook has been set up to be used with mkinitcpio and has been tested solely on an Arch Linux x86_64 installation.

## Prerquisites
 - The hook does not work together with the `systemd` hook in `/etc/mkinitcpio.conf`
 - For this hook to operate, the following packages are required: `dbus, bluez, bluez-utils`
 - It relies on the `AutoEnable=true` setting in `/etc/bluetooth/main.conf`
 - Please be aware that running this hook will increase your initramfs and fallback images in size, so be prepared for that

## Preparations
 1. If you haven't already, make sure you have paired, connected and trusted your bluetooth keyboard. Instructions can be found on the ArchWiki [here](https://wiki.archlinux.org/index.php/bluetooth#Pairing).
 2. Ensure both your bluetooth keyboard and your system startup process are operational without issues at this point
 3. Check that `AutoEnable` is enabled in `/etc/bluetooth/main.conf`

## Setup

 1. Download or clone this repository to your machine and change into it
 2. Run `makepkg` to install this hook
 4. Add `bluetooth` to your HOOKS array in `/etc/mkinitcpio.conf` before `encrypt` and after `keyboard`
 5. Rebuild your initramfs with `mkinitcpio`
 6. Upon next reboot, your keyboard should become operational automatically just before cryptsetup asks for your passphrase
