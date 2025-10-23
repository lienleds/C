# Chainloading

Chainloading is the process of loading one bootloader from another. It is commonly used in dual-boot setups to allow multiple operating systems to coexist on the same machine.

## How It Works
1. The primary bootloader loads and executes the secondary bootloader.
2. The secondary bootloader then loads the operating system.

## Use Cases
- Dual-boot setups.
- Testing different bootloaders.
- Booting from external devices.

## Example
- GRUB can chainload another bootloader, such as Windows Boot Manager.

## Additional Resources
- [GRUB Chainloading](https://www.gnu.org/software/grub/manual/)