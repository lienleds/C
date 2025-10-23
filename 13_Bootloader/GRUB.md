# GRUB (GRand Unified Bootloader)

GRUB is one of the most popular and versatile bootloaders used in modern systems. It supports multiple operating systems and provides extensive configurability.

## Key Features
- **Multi-OS Support**: GRUB can boot multiple operating systems, making it ideal for dual-boot setups.
- **Highly Configurable**: Offers a wide range of options for customizing the boot process.
- **Interactive Shell**: Provides a command-line interface for troubleshooting and advanced configuration.
- **Support for Modern Systems**: Compatible with both BIOS and UEFI firmware.

## GRUB Workflow

1. **Stage 1: BIOS/UEFI Loads GRUB**
   - The BIOS/UEFI firmware initializes hardware and loads the GRUB Stage 1 bootloader from the Master Boot Record (MBR) or EFI partition.

2. **Stage 2: GRUB Menu**
   - GRUB displays a menu of available operating systems or kernels.
   - Users can select an entry or modify boot parameters interactively.

3. **Stage 3: Load Kernel**
   - GRUB loads the selected kernel into memory.
   - It passes the necessary boot parameters to the kernel.

4. **Stage 4: Transfer Control**
   - GRUB transfers control to the operating system kernel, which initializes the system.

## GRUB Configuration

The GRUB configuration file is typically located at `/etc/grub2.cfg` or `/boot/grub/grub.cfg`. It defines the boot menu entries and other settings.

### Example GRUB Entry
```bash
menuentry 'My Linux OS' {
    set root=(hd0,1)
    linux /vmlinuz root=/dev/sda1
    initrd /initrd.img
}
```

## Common GRUB Commands

- **Install GRUB**:
  ```bash
  sudo grub-install /dev/sda
  ```
- **Update GRUB Configuration**:
  ```bash
  sudo update-grub
  ```
- **Access GRUB Shell**:
  Press `c` at the GRUB menu to access the command-line interface.

## Exercises

1. Identify the bootloader used on your system.
2. Modify the GRUB configuration to add a custom boot entry.
3. Explore the GRUB shell and experiment with its commands.
4. Set up a dual-boot system using GRUB.
5. Secure GRUB by setting a password for the boot menu.

## Additional Resources

- [GNU GRUB Documentation](https://www.gnu.org/software/grub/manual/)
- [Arch Linux GRUB Wiki](https://wiki.archlinux.org/title/GRUB)
- [GRUB Command Reference](https://www.gnu.org/software/grub/manual/grub/html_node/Command_002dline-and-menu-entry-command-list.html)