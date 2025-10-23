# Linux Upstart

`Upstart` is an event-based init system used in some Linux distributions before the adoption of `systemd`. It was designed to handle the starting of tasks and services during boot, stopping them during shutdown, and supervising them while the system is running.

## Key Features

1. **Event-Driven**:
   - Upstart uses events to manage services. For example, a service can be started when a specific event occurs, such as mounting a filesystem.

2. **Parallel Service Startup**:
   - Services can be started in parallel, reducing boot times compared to traditional init systems like SysV.

3. **Job Configuration Files**:
   - Jobs are defined in configuration files located in `/etc/init/`.
   - Example job file:
     ```conf
     # Example job file
     description "My Custom Service"

     start on filesystem
     stop on runlevel [016]

     script
         exec /path/to/your/program
     end script
     ```

4. **Backward Compatibility**:
   - Upstart provides compatibility with SysV init scripts, allowing older scripts to work without modification.

## Example: Creating a Custom Job

1. Create a job file in `/etc/init/`:
   ```bash
   sudo nano /etc/init/my_service.conf
   ```
2. Add the following content:
   ```conf
   description "My Custom Service"

   start on filesystem
   stop on runlevel [016]

   script
       exec /path/to/your/program
   end script
   ```
3. Start the service:
   ```bash
   sudo start my_service
   ```
4. Stop the service:
   ```bash
   sudo stop my_service
   ```

## Exercises

1. Create a custom job that starts a script when the system boots.
2. Experiment with different events to trigger job execution.
3. Compare Upstart with SysV and `systemd` in terms of service management.

## Additional Resources

- [Upstart Documentation](http://upstart.ubuntu.com/)
- [Upstart Cookbook](http://upstart.ubuntu.com/cookbook/)