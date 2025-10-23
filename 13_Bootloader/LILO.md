# LILO (Linux Loader)

LILO is a simple and legacy bootloader that was widely used in older Linux systems. While it has been largely replaced by GRUB, it remains an important part of Linux history and is still used in some niche scenarios.

## Key Features
- **Simplicity**: LILO is straightforward and easy to configure.
- **Direct Kernel Loading**: Loads the operating system kernel directly without an intermediate menu.
- **Legacy Support**: Suitable for older systems that do not require advanced bootloader features.
- **Compact Size**: Minimalistic design with a small footprint.

## LILO Workflow

1. **Stage 1: BIOS Loads LILO**
   - The BIOS loads the LILO bootloader from the Master Boot Record (MBR).

2. **Stage 2: Load Kernel**
   - LILO directly loads the operating system kernel specified in its configuration file.

3. **Stage 3: Transfer Control**
   - LILO transfers control to the kernel, which initializes the system.

## LILO Configuration

The LILO configuration file is typically located at `/etc/lilo.conf`. It defines the kernel and boot options.

### Example LILO Configuration
```bash
boot=/dev/sda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
default=linux

image=/boot/vmlinuz
  label=linux
  read-only
  root=/dev/sda1
```

## Common LILO Commands

- **Install LILO**:
  ```bash
  sudo lilo
  ```
- **View LILO Configuration**:
  ```bash
  cat /etc/lilo.conf
  ```
- **Update LILO**:
  After modifying the configuration file, run:
  ```bash
  sudo lilo
  ```

## Exercises

1. Install LILO on a virtual machine and configure it to boot a Linux kernel.
2. Modify the LILO configuration file to add a custom boot option.
3. Compare the boot process of LILO with GRUB.
4. Investigate the limitations of LILO in modern systems.

## Additional Resources

- [LILO Documentation](https://lilo.alioth.debian.org/)
- [Arch Linux LILO Wiki](https://wiki.archlinux.org/title/LILO)
- [Linux Boot Process](https://www.tldp.org/HOWTO/BootPrompt-HOWTO.html)