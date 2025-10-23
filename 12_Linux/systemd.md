# Linux systemd

`systemd` is a system and service manager for Linux operating systems. It is responsible for initializing the system, managing services, and handling dependencies.

## Key Features

1. **Service Management**:
   - Start, stop, enable, and disable services.
   - Example commands:
     ```bash
     systemctl start service_name
     systemctl stop service_name
     systemctl enable service_name
     systemctl disable service_name
     ```

2. **Unit Files**:
   - `systemd` uses unit files to define services, targets, and other resources.
   - Example of a service unit file:
     ```ini
     [Unit]
     Description=My Custom Service

     [Service]
     ExecStart=/path/to/your/program

     [Install]
     WantedBy=multi-user.target
     ```

3. **Logging**:
   - `systemd` integrates with `journald` for logging.
   - View logs with:
     ```bash
     journalctl -u service_name
     ```

4. **Targets**:
   - Targets group units together, similar to runlevels in traditional init systems.
   - Example:
     ```bash
     systemctl isolate multi-user.target
     ```

## Understanding systemd: A Step-by-Step Guide for Beginners

### 1. What is systemd?
`systemd` is a modern system and service manager for Linux. It was introduced to replace the traditional init systems like System V (SysV) and Upstart. It provides faster boot times, better dependency handling, and a unified way to manage services.

### 2. Why was systemd introduced?
Before `systemd`, Linux systems used SysV or Upstart for initialization. These systems had limitations:
- **SysV**: Relied on shell scripts for service management, which were slow and hard to maintain.
- **Upstart**: Improved over SysV but lacked features like dependency resolution.

`systemd` was designed to address these issues by:
- Using binary unit files for faster processing.
- Providing parallel service startup.
- Offering a unified interface for managing services, logging, and targets.

### 3. Key Concepts for Beginners

#### a. Unit Files
Unit files are configuration files that define how services, targets, and other resources are managed. They are stored in:
- `/etc/systemd/system/` (custom unit files)
- `/lib/systemd/system/` (default unit files)

#### b. Targets
Targets group units together. For example:
- `multi-user.target`: Multi-user mode without GUI.
- `graphical.target`: Multi-user mode with GUI.

#### c. Journald
`journald` is the logging system integrated with `systemd`. It provides detailed logs for debugging.

### 4. Getting Started with systemd

#### Step 1: Check the Status of a Service
```bash
systemctl status service_name
```
Example:
```bash
systemctl status sshd
```

#### Step 2: Start and Stop a Service
```bash
systemctl start service_name
systemctl stop service_name
```

#### Step 3: Enable a Service to Start on Boot
```bash
systemctl enable service_name
```

#### Step 4: View Logs for a Service
```bash
journalctl -u service_name
```

### 5. Example: Creating and Managing a Custom Service

#### a. Create a Script
Create a simple script to be managed by `systemd`:
```bash
sudo nano /usr/local/bin/hello_world.sh
```
Add the following content:
```bash
#!/bin/bash
echo "Hello, World!"
```
Make the script executable:
```bash
sudo chmod +x /usr/local/bin/hello_world.sh
```

#### b. Create a Unit File
Create a unit file for the script:
```bash
sudo nano /etc/systemd/system/hello_world.service
```
Add the following content:
```ini
[Unit]
Description=Hello World Service

[Service]
ExecStart=/usr/local/bin/hello_world.sh

[Install]
WantedBy=multi-user.target
```

#### c. Reload systemd and Start the Service
```bash
sudo systemctl daemon-reload
sudo systemctl start hello_world.service
```

#### d. Enable the Service to Start on Boot
```bash
sudo systemctl enable hello_world.service
```

## Example: Creating a Custom Service

1. Create a service file:
   ```bash
   sudo nano /etc/systemd/system/my_service.service
   ```
2. Add the following content:
   ```ini
   [Unit]
   Description=My Custom Service

   [Service]
   ExecStart=/path/to/your/program

   [Install]
   WantedBy=multi-user.target
   ```
3. Reload `systemd`:
   ```bash
   sudo systemctl daemon-reload
   ```
4. Start the service:
   ```bash
   sudo systemctl start my_service
   ```
5. Enable the service to start on boot:
   ```bash
   sudo systemctl enable my_service
   ```

## Exercises

1. Create a custom service that runs a simple script on boot.
2. Use `journalctl` to debug a failing service.
3. Experiment with different targets and observe their effects.
4. Create a service that runs a Python script on boot.
5. Use `journalctl` to debug a service that fails to start.
6. Experiment with different targets and observe their effects.

## Additional Resources

- [systemd Documentation](https://www.freedesktop.org/wiki/Software/systemd/)
- [systemctl Cheat Sheet](https://www.freedesktop.org/software/systemd/man/systemctl.html)