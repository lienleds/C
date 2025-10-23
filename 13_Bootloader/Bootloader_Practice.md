# Bootloader Practice

This document provides practical exercises and examples to help you understand and work with bootloaders. These exercises are designed to reinforce the concepts covered in the bootloader documentation.

## Prerequisites

Before starting, ensure you have the following:
- A basic understanding of bootloaders (BIOS, UEFI, GRUB, etc.).
- A system with virtualization enabled or a physical machine for testing.
- Tools like QEMU, GRUB, and a Linux distribution ISO.

## Exercises

### 1. Create a Bootable USB Drive
1. Download a Linux distribution ISO (e.g., Ubuntu, Fedora).
2. Use the `dd` command to create a bootable USB drive:
   ```bash
   sudo dd if=linux.iso of=/dev/sdX bs=4M
   ```
   Replace `linux.iso` with the path to your ISO file and `/dev/sdX` with your USB device.
3. Boot your system from the USB drive and verify the installation process.

### 2. Install and Configure GRUB
1. Install GRUB on your system:
   ```bash
   sudo grub-install /dev/sda
   ```
2. Edit the GRUB configuration file to add a custom boot entry:
   ```bash
   sudo nano /etc/grub.d/40_custom
   ```
   Add the following entry:
   ```bash
   menuentry 'Custom Linux' {
       set root=(hd0,1)
       linux /vmlinuz root=/dev/sda1
       initrd /initrd.img
   }
   ```
3. Update GRUB:
   ```bash
   sudo update-grub
   ```
4. Reboot and select the custom entry from the GRUB menu.

### 3. Chainloading
1. Install a secondary bootloader (e.g., Windows Boot Manager) on a separate partition.
2. Configure GRUB to chainload the secondary bootloader:
   ```bash
   menuentry 'Windows Boot Manager' {
       set root=(hd0,2)
       chainloader +1
   }
   ```
3. Reboot and test the chainloading setup.

### 4. Debugging a Bootloader
1. Use QEMU to emulate a virtual machine:
   ```bash
   qemu-system-x86_64 -hda mydisk.qcow2 -cdrom myos.iso -boot d -m 1024
   ```
2. Add debug messages to your bootloader code.
3. Use GDB to debug the bootloader:
   ```bash
   gdb -ex "target remote :1234" -ex "symbol-file bootloader.elf"
   ```

### 5. Secure Boot
1. Enable Secure Boot in your UEFI firmware settings.
2. Sign your bootloader with a trusted key:
   ```bash
   sbsign --key db.key --cert db.crt --output bootloader.efi.signed bootloader.efi
   ```
3. Add the key to the firmware key database.
4. Test the Secure Boot setup by booting the signed bootloader.

## Additional Resources
- [GRUB Manual](https://www.gnu.org/software/grub/manual/)
- [UEFI Secure Boot](https://uefi.org/specifications)
- [QEMU Documentation](https://www.qemu.org/documentation/)

## Notes
- Always test bootloader configurations in a virtual machine before applying them to a physical system.
- Keep a backup of your system and important data before experimenting with bootloaders.