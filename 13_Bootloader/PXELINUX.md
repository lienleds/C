# PXELINUX

PXELINUX is a variant of SYSLINUX designed for network booting using the Preboot Execution Environment (PXE). It is commonly used for diskless workstations, network installations, and other scenarios where booting over a network is required.

## Key Features
- **Network Booting**: Boots systems over a network using PXE.
- **Part of SYSLINUX**: Shares features and configuration style with SYSLINUX.
- **Customizable**: Supports advanced boot options and scripting.
- **Lightweight**: Minimal resource requirements, making it ideal for network environments.

## PXELINUX Workflow

1. **Set Up a PXE Server**:
   - Configure a DHCP server to provide PXE boot options.
   - Set up a TFTP server to host the PXELINUX bootloader and configuration files.

2. **Configure PXELINUX**:
   - Create a `pxelinux.cfg` file to specify the kernel and boot parameters.

3. **Boot the System**:
   - Boot the client system over the network and select the desired boot option.

## PXELINUX Commands

- **Install PXELINUX**:
  Copy the PXELINUX binary to the TFTP server root directory:
  ```bash
  cp /usr/lib/syslinux/pxelinux.0 /var/lib/tftpboot/
  ```

- **Set Up DHCP for PXE Booting**:
  Add the following to your DHCP server configuration:
  ```bash
  filename "pxelinux.0";
  next-server 192.168.1.1;
  ```

- **Test PXE Boot**:
  Boot a client system configured for network booting and verify the PXELINUX menu appears.

## PXELINUX Configuration

The PXELINUX configuration file (`pxelinux.cfg/default`) defines the boot menu and kernel parameters. It is stored on the TFTP server.

### Example PXELINUX Configuration
```bash
DEFAULT linux
LABEL linux
  KERNEL vmlinuz
  APPEND initrd=initrd.img root=/dev/nfs nfsroot=192.168.1.100:/nfsroot
```

## Exercises

1. Set up a PXE server and use PXELINUX to boot a diskless workstation.
2. Modify the `pxelinux.cfg` file to add multiple boot options.
3. Compare PXELINUX with other network boot solutions in terms of ease of use and features.
4. Investigate the security implications of PXE booting and explore ways to secure the process.

## Additional Resources

- [PXELINUX Documentation](https://www.syslinux.org/wiki/index.php?title=PXELINUX)
- [Arch Linux PXE Wiki](https://wiki.archlinux.org/title/PXE)
- [TFTP Server Setup](https://wiki.archlinux.org/title/TFTP)