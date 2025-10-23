# Linux System V (SysV)

`System V` (SysV) is a traditional init system used in older Linux distributions. It is responsible for initializing the system and managing services during boot.

## Key Features

1. **Runlevels**:
   - SysV uses runlevels to define the state of the system.
   - Common runlevels:
     - `0`: Halt
     - `1`: Single-user mode
     - `3`: Multi-user mode without GUI
     - `5`: Multi-user mode with GUI
     - `6`: Reboot
   - Change runlevels with:
     ```bash
     init 3
     ```

2. **Init Scripts**:
   - Services are managed using shell scripts located in `/etc/init.d/`.
   - Example commands:
     ```bash
     /etc/init.d/service_name start
     /etc/init.d/service_name stop
     ```

3. **Service Management**:
   - Use `service` command to manage services:
     ```bash
     service service_name start
     service service_name stop
     ```

4. **Startup Scripts**:
   - Scripts are linked to runlevels using symbolic links in `/etc/rc.d/`.
   - Example:
     ```bash
     ln -s /etc/init.d/my_service /etc/rc.d/rc3.d/S99my_service
     ```

## Understanding System V Init: A Step-by-Step Guide for Beginners

### 1. What is System V Init?
System V Init (SysV) is one of the earliest init systems used in Linux. It is responsible for initializing the system, starting services, and managing runlevels during the boot process.

### 2. Why is SysV Important?
SysV was widely used in older Linux distributions and provides a simple, script-based approach to service management. While modern systems like `systemd` have replaced SysV, understanding it is essential for working with legacy systems.

### 3. Key Concepts for Beginners

#### a. Runlevels
Runlevels define the state of the system. Each runlevel corresponds to a specific mode of operation:
- `0`: Halt (shutdown the system).
- `1`: Single-user mode (maintenance mode).
- `3`: Multi-user mode without GUI.
- `5`: Multi-user mode with GUI.
- `6`: Reboot.

To check the current runlevel:
```bash
runlevel
```
To change the runlevel:
```bash
init 3
```

#### b. Init Scripts
Init scripts are shell scripts located in `/etc/init.d/`. These scripts define how services are started, stopped, and restarted.

#### c. Startup Scripts
Startup scripts are symbolic links in `/etc/rc.d/` that point to init scripts. These links are organized by runlevel directories (e.g., `/etc/rc.d/rc3.d/` for runlevel 3).

### 4. Getting Started with SysV

#### Step 1: Check the Status of a Service
```bash
service service_name status
```
Example:
```bash
service sshd status
```

#### Step 2: Start and Stop a Service
```bash
service service_name start
service service_name stop
```

#### Step 3: Add a Service to a Runlevel
To add a service to a specific runlevel, create a symbolic link:
```bash
ln -s /etc/init.d/service_name /etc/rc.d/rc3.d/S99service_name
```

#### Step 4: Create a Custom Init Script
1. Create a script in `/etc/init.d/`:
   ```bash
   sudo nano /etc/init.d/my_service
   ```
2. Add the following content:
   ```bash
   #!/bin/bash
   # My Custom Service

   case "$1" in
       start)
           echo "Starting my service..."
           # Command to start your service
           ;;
       stop)
           echo "Stopping my service..."
           # Command to stop your service
           ;;
       restart)
           $0 stop
           $0 start
           ;;
       *)
           echo "Usage: $0 {start|stop|restart}"
           exit 1
   esac

   exit 0
   ```
3. Make the script executable:
   ```bash
   sudo chmod +x /etc/init.d/my_service
   ```
4. Add the script to the desired runlevel:
   ```bash
   sudo ln -s /etc/init.d/my_service /etc/rc.d/rc3.d/S99my_service
   ```
5. Start the service:
   ```bash
   sudo service my_service start
   ```

### 5. Exercises for Beginners
1. Create a custom init script to manage a simple service.
2. Experiment with different runlevels and observe their effects.
3. Compare SysV with `systemd` in terms of service management.

### 6. Additional Tips
- Use `man init` to explore more about runlevels.
- Check `/var/log/` for logs related to services.
- Use `chkconfig` (if available) to manage services across runlevels.

## Example: Creating a Custom Init Script

1. Create a script in `/etc/init.d/`:
   ```bash
   sudo nano /etc/init.d/my_service
   ```
2. Add the following content:
   ```bash
   #!/bin/bash
   # My Custom Service

   case "$1" in
       start)
           echo "Starting my service..."
           # Command to start your service
           ;;
       stop)
           echo "Stopping my service..."
           # Command to stop your service
           ;;
       restart)
           $0 stop
           $0 start
           ;;
       *)
           echo "Usage: $0 {start|stop|restart}"
           exit 1
   esac

   exit 0
   ```
3. Make the script executable:
   ```bash
   sudo chmod +x /etc/init.d/my_service
   ```
4. Add the script to the desired runlevel:
   ```bash
   sudo ln -s /etc/init.d/my_service /etc/rc.d/rc3.d/S99my_service
   ```
5. Start the service:
   ```bash
   sudo service my_service start
   ```

## Exercises

1. Create a custom init script to manage a simple service.
2. Experiment with different runlevels and observe their effects.
3. Compare SysV with systemd in terms of service management.

## Additional Resources

- [SysVinit Documentation](https://wiki.debian.org/Init)
- [Linux Runlevels](https://tldp.org/HOWTO/From-PowerUp-To-Bash-Prompt-HOWTO-6.html)