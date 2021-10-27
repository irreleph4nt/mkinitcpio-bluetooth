# mkinitcpio-bluetooth
mkinitcpio hook to enable bluetooth connectivity during boot.

# Instructions
This hook has been set up to be used with mkinitcpio and has been tested solely on an Arch Linux x86_64 installation that uses refind-efi **instead of GRUB**.

## Prerquisites
 - The hook does not work together with the `systemd` hook in `/etc/mkinitcpio.conf`
 - For this hook to operate, the following packages are required: `dbus, bluez, bluez-utils`
 - It relies on the `AutoEnable=true` setting in `/etc/bluetooth/main.conf`
 
### Boot process & a note for Manjaro users
Please be aware that just like any other additional module, the hook adds to your kernel image. To operate, it hence requires your kernel to be available during boot, **before** you are asked for a passphrase.
A supported setup therefore strictly requires your /boot partition to **not** be encrypted.

If you are a **Manjaro** user and installed your system using their setup assistant, there is a high likelyhood of your /boot partition also being encrypted. In that case this hook won't work for you as you are prompted by GRUB early on, *before* your kernel and hence this module is available. Please refer to [this](https://forum.manjaro.org/t/full-system-encryption-without-encrypted-boot/113445) Manjaro post for options to make your boot process support this hook.


## Preparations
 1. If you haven't already, make sure you have paired, connected and trusted your bluetooth keyboard. Instructions can be found on the ArchWiki [here](https://wiki.archlinux.org/index.php/bluetooth#Pairing).
 2. Ensure both your bluetooth keyboard and your system startup process are operational without issues at this point
 3. Check that `AutoEnable` is enabled in `/etc/bluetooth/main.conf`

## Setup
 1. Download or clone this repository to your machine and change into it
 2. Run `makepkg` to install this hook
 3. Add `bluetooth` to your HOOKS array in `/etc/mkinitcpio.conf` before `encrypt` and after `keyboard`
 
    **Example:** `HOOKS=(base udev autodetect modconf keyboard keymap bluetooth block encrypt lvm2 filesystems fsck)`
 4. **(if needed)** Add any file, binary, module that your keyboard or bt adapter might need
 
    **Example:** 
    ```
    FILES=(/usr/lib/firmware/intel/ibt-20-1-3.sfi) 
    MODULES=(usbhid xhci_hcd)
    ```
 5. Rebuild your initramfs with `mkinitcpio`
 6. Upon next reboot, your keyboard should become operational automatically just before cryptsetup asks for your passphrase

## Troubleshooting
If you have trouble finding what module, file, binary you need for your keyboard or bt adapter, try looking for errors in dmesg and journalctl related to bluetooth.

**Example:**
```
# journactl | grep bluetooth
kernel: bluetooth hci0: Direct firmware load for intel/ibt-20-1-3.sfi failed with error -2
# dmesg | grep bluetooth
[    1.717123] bluetooth hci0: Direct firmware load for intel/ibt-20-1-3.sfi failed with error -2
```
