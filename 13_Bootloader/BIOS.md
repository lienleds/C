# BIOS (Basic Input/Output System)

The Basic Input/Output System (BIOS) is firmware used to perform hardware initialization during the booting process and to provide runtime services for operating systems and programs. It is the first software that runs when a computer is powered on.

## Key Features
- **Hardware Initialization**: Initializes hardware components such as the CPU, memory, and peripherals.
- **Bootloader Execution**: Loads the bootloader from the Master Boot Record (MBR) or other bootable media.
- **Legacy Support**: Compatible with older systems and operating systems.
- **Configuration Interface**: Provides a setup utility for configuring hardware settings.

## BIOS Workflow

1. **Power-On Self-Test (POST)**:
   - The BIOS performs a POST to verify that hardware components are functioning correctly.

2. **Hardware Initialization**:
   - Initializes the CPU, memory, and peripherals.

3. **Boot Device Selection**:
   - Determines the boot device order based on the BIOS configuration.

4. **Bootloader Execution**:
   - Loads the bootloader from the MBR or other bootable media.

5. **Operating System Boot**:
   - Transfers control to the bootloader, which loads the operating system kernel.

## Advantages of BIOS

- **Simplicity**:
  - Provides a straightforward interface for hardware initialization and booting.

- **Compatibility**:
  - Supported by a wide range of legacy systems and operating systems.

- **User Configuration**:
  - Allows users to configure hardware settings through the BIOS setup utility.

## Limitations of BIOS

- **Slow Boot Times**:
  - BIOS initializes hardware sequentially, leading to slower boot times compared to UEFI.

- **Limited Disk Support**:
  - Supports only MBR partitioning, which is limited to 2 TB disks.

- **No Secure Boot**:
  - Lacks modern security features like Secure Boot, which are available in UEFI.

## Exercises

1. Access the BIOS setup utility on your system and explore its configuration options.
2. Change the boot order in the BIOS to boot from a USB drive.
3. Compare the BIOS with UEFI in terms of features and limitations.
4. Investigate the POST process and identify the hardware checks performed by the BIOS.

## Additional Resources

- [Wikipedia: BIOS](https://en.wikipedia.org/wiki/BIOS)
- [BIOS vs UEFI](https://www.howtogeek.com/56958/)
- [Understanding POST](https://www.computerhope.com/jargon/p/post.htm)
- [BIOS Configuration Guide](https://www.pcworld.com/article/241032/how-to-enter-your-pcs-bios.html)