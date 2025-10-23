# Coreboot

Coreboot is an open-source firmware replacement for proprietary BIOS/UEFI. It is designed to be lightweight, fast, and highly customizable, making it ideal for Chromebooks, servers, and custom hardware platforms.

## Key Features
- **Open Source**: Fully open-source firmware, allowing for transparency and community contributions.
- **Fast Boot Times**: Optimized for minimal boot times by initializing only essential hardware components.
- **Customizable**: Can be tailored for specific hardware platforms and use cases.
- **Payload Support**: Coreboot uses payloads like SeaBIOS, GRUB, or Linux to provide additional functionality.
- **Security**: Offers advanced security features, including measured boot and verified boot.

## Coreboot Workflow

1. **Build Coreboot**:
   - Use the Coreboot build system to compile a firmware image tailored to your hardware.

2. **Flash Coreboot**:
   - Flash the compiled firmware image to the device using a hardware programmer or software tool.

3. **Boot the System**:
   - Coreboot initializes the hardware and loads the payload, which then boots the operating system.

## Coreboot Commands

- **Build Coreboot**:
  ```bash
  make menuconfig
  make
  ```

- **Flash Coreboot**:
  ```bash
  flashrom -p internal -w coreboot.rom
  ```

- **Verify Coreboot Installation**:
  ```bash
  cbmem -c
  ```

## Coreboot Configuration

Coreboot is configured using the `menuconfig` interface, which allows users to select hardware options, payloads, and other settings.

### Example Coreboot Configuration Steps
1. Run `make menuconfig` to open the configuration interface.
2. Select the target hardware platform.
3. Choose a payload (e.g., SeaBIOS, GRUB, or Linux).
4. Save the configuration and exit.

## Exercises

1. Build and flash Coreboot on a supported device.
2. Compare the boot time of Coreboot with traditional BIOS/UEFI implementations.
3. Explore the Coreboot payload options and configure a custom payload.
4. Investigate the security features of Coreboot, such as verified boot.
5. Test Coreboot on a virtual machine before deploying it on physical hardware.

## Additional Resources

- [Coreboot Project](https://www.coreboot.org/)
- [Coreboot Documentation](https://doc.coreboot.org/)
- [Flashrom Utility](https://www.flashrom.org/)
- [SeaBIOS Payload](https://www.seabios.org/)
- [Verified Boot](https://www.coreboot.org/Verified_Boot)