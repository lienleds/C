# GUID Partition Table (GPT)

The GUID Partition Table (GPT) is a modern partitioning scheme that overcomes the limitations of the Master Boot Record (MBR). It is part of the UEFI (Unified Extensible Firmware Interface) standard and is designed for use with modern systems.

## Key Features
- **Large Disk Support**: Supports disks larger than 2 TB.
- **Unlimited Partitions**: Allows for virtually unlimited partitions (limited by the operating system).
- **Redundancy**: Stores a backup of the partition table at the end of the disk.
- **Unique Identifiers**: Uses globally unique identifiers (GUIDs) for partitions.
- **Modern Compatibility**: Designed for UEFI systems but can also work with legacy BIOS systems.

## Structure of GPT

The GPT structure includes the following components:

1. **Protective MBR**:
   - A legacy MBR at the beginning of the disk to prevent older tools from misinterpreting the disk.

2. **Primary GPT Header**:
   - Located at the beginning of the disk.
   - Contains metadata about the partition table, such as the disk GUID and the location of partition entries.

3. **Partition Entries**:
   - A table of partition entries, each describing a partition's type, GUID, starting and ending sectors, and attributes.

4. **Backup GPT Header**:
   - A copy of the primary GPT header stored at the end of the disk for redundancy.

## GPT Workflow

1. **UEFI/BIOS Execution**:
   - The firmware initializes hardware and reads the GPT header from the disk.

2. **Partition Table Parsing**:
   - The firmware or operating system reads the partition entries to identify available partitions.

3. **Operating System Boot**:
   - The bootloader loads the operating system kernel from the specified partition.

## Advantages of GPT

- **Supports Large Disks**:
  - Can handle disks larger than 2 TB, unlike MBR.

- **More Partitions**:
  - Allows for more than four primary partitions without the need for extended partitions.

- **Redundancy**:
  - Stores a backup of the partition table for improved reliability.

- **Improved Metadata**:
  - Uses GUIDs and descriptive partition types for better management.

## Exercises

1. Inspect the GPT of a disk using tools like `gdisk` or `parted`.
2. Create and manage partitions on a GPT-formatted disk.
3. Compare GPT with MBR in terms of features and limitations.
4. Explore the redundancy features of GPT by simulating a failure of the primary GPT header.

## Additional Resources

- [Wikipedia: GUID Partition Table](https://en.wikipedia.org/wiki/GUID_Partition_Table)
- [GPT vs MBR](https://www.howtogeek.com/193669/whats-the-difference-between-mbr-and-gpt/)
- [Linux parted Command](https://man7.org/linux/man-pages/man8/parted.8.html)
- [UEFI Specification](https://uefi.org/specifications)