# SYSLINUX

SYSLINUX is a lightweight bootloader designed for booting from removable media such as USB drives, CDs, and other FAT file systems. It is part of the SYSLINUX Project, which includes PXELINUX and other variants.

## Key Features
- **Target Use Case**: Ideal for live USBs, rescue disks, and lightweight systems.
- **Simple Configuration**: Uses a plain text configuration file (e.g., `syslinux.cfg`).
- **Chainloading**: Supports booting other bootloaders or operating systems.
- **Modular Design**: Includes variants like PXELINUX for network booting and ISOLINUX for booting from ISO images.

## SYSLINUX Workflow

1. **Install SYSLINUX**:
   - Use the `syslinux` command to install the bootloader on a USB drive or other media.

2. **Configure SYSLINUX**:
   - Edit the `syslinux.cfg` file to specify the kernel and boot parameters.

3. **Boot the System**:
   - Insert the bootable media and boot the system.

## SYSLINUX Commands

- **Install SYSLINUX**:
  ```bash
  syslinux /dev/sdX1
  ```
  Replace `/dev/sdX1` with the partition where SYSLINUX should be installed.

- **Create a Bootable USB Drive**:
  ```bash
  dd if=/path/to/syslinux.img of=/dev/sdX bs=4M
  ```

- **View SYSLINUX Version**:
  ```bash
  syslinux --version
  ```

## SYSLINUX Configuration

The SYSLINUX configuration file (`syslinux.cfg`) defines the boot menu and kernel parameters. It is typically located in the root directory of the bootable media.

### Example SYSLINUX Configuration
```bash
DEFAULT linux
LABEL linux
  KERNEL vmlinuz
  APPEND initrd=initrd.img root=/dev/sda1
```

## Exercises

1. Create a bootable USB drive using SYSLINUX and test it on a virtual machine.
2. Modify the `syslinux.cfg` file to add a custom boot option.
3. Compare SYSLINUX with other bootloaders like GRUB and LILO in terms of simplicity and use cases.
4. Explore the modular variants of SYSLINUX, such as PXELINUX and ISOLINUX.

## Additional Resources

- [SYSLINUX Project](https://www.syslinux.org/)
- [Arch Linux SYSLINUX Wiki](https://wiki.archlinux.org/title/SYSLINUX)
- [Bootloader Basics](https://wiki.archlinux.org/title/Boot_loader)