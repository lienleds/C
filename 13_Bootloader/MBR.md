# Master Boot Record (MBR)

The Master Boot Record (MBR) is a special type of boot sector located at the very beginning of a storage device, such as a hard disk or SSD. It contains the information necessary to boot the operating system and manage disk partitions.

## Key Features
- **Bootloader Storage**: The MBR contains the first stage of the bootloader, which is executed by the BIOS.
- **Partition Table**: Stores information about the disk's primary partitions.
- **Compatibility**: Supported by most legacy systems and operating systems.
- **Size Limitation**: Limited to 2 TB disks and supports up to four primary partitions.

## Structure of the MBR

The MBR is 512 bytes in size and is divided into the following sections:

1. **Bootloader Code (446 bytes)**:
   - Contains the first stage of the bootloader.
   - Responsible for loading the second stage of the bootloader or the operating system.

2. **Partition Table (64 bytes)**:
   - Describes up to four primary partitions on the disk.
   - Each partition entry is 16 bytes long.

3. **Boot Signature (2 bytes)**:
   - A marker (0x55AA) indicating that the sector contains a valid MBR.

## MBR Workflow

1. **BIOS Execution**:
   - The BIOS initializes hardware and reads the MBR from the first sector of the boot device.

2. **Bootloader Execution**:
   - The bootloader code in the MBR is executed.
   - It loads the second stage of the bootloader or directly boots the operating system.

3. **Operating System Boot**:
   - The operating system kernel is loaded into memory and executed.

## Limitations of MBR

- **Partition Limitations**:
  - Supports only four primary partitions.
  - Extended partitions can be used to overcome this limitation, but they add complexity.

- **Disk Size Limitation**:
  - Limited to disks of up to 2 TB due to the 32-bit addressing scheme.

- **Legacy Support**:
  - Not suitable for modern systems that use UEFI and GPT (GUID Partition Table).

## Exercises

1. Inspect the MBR of a disk using a hex editor.
2. Create and manage partitions on an MBR-formatted disk using tools like `fdisk`.
3. Compare the MBR with GPT in terms of features and limitations.
4. Write a simple bootloader and install it in the MBR of a virtual disk.

## Additional Resources

- [Wikipedia: Master Boot Record](https://en.wikipedia.org/wiki/Master_boot_record)
- [MBR vs GPT](https://www.howtogeek.com/193669/whats-the-difference-between-mbr-and-gpt/)
- [Linux fdisk Command](https://man7.org/linux/man-pages/man8/fdisk.8.html)
- [Writing a Simple Bootloader](https://wiki.osdev.org/MBR)