# Common Linux Commands

This document provides a comprehensive list of commonly used Linux commands, categorized for easy reference. Each command includes a brief description and examples.

## 1. Navigating the Filesystem
- `ls`: List files and directories.
  ```bash
  ls -la
  ```
- `cd`: Change directory.
  ```bash
  cd /home/user
  ```
- `pwd`: Print the current working directory.
  ```bash
  pwd
  ```
- `mkdir`: Create a new directory.
  ```bash
  mkdir new_folder
  ```
- `rm`: Remove files or directories.
  ```bash
  rm file.txt
  rm -r folder_name
  ```

## 2. File Operations
- `cp`: Copy files or directories.
  ```bash
  cp source.txt destination.txt
  cp -r source_folder/ destination_folder/
  ```
- `mv`: Move or rename files.
  ```bash
  mv old_name.txt new_name.txt
  ```
- `cat`: Display file contents.
  ```bash
  cat file.txt
  ```
- `nano` or `vim`: Edit files.
  ```bash
  nano file.txt
  vim file.txt
  ```

## 3. Process Management
- `ps`: Display running processes.
  ```bash
  ps aux
  ```
- `top`: Monitor system resources.
  ```bash
  top
  ```
- `kill`: Terminate a process.
  ```bash
  kill 1234
  ```

## 4. Permissions and Ownership
- `chmod`: Change file permissions.
  ```bash
  chmod +x script.sh
  ```
- `chown`: Change file ownership.
  ```bash
  chown user:group file.txt
  ```
- `sudo`: Execute commands as the superuser.
  ```bash
  sudo apt update
  ```

## 5. Networking
- `ping`: Test network connectivity.
  ```bash
  ping google.com
  ```
- `ifconfig` or `ip`: Display network configuration.
  ```bash
  ifconfig
  ip addr
  ```
- `curl`: Transfer data from or to a server.
  ```bash
  curl https://example.com
  ```

## 6. Package Management
- `apt`: Package manager for Debian-based systems.
  ```bash
  sudo apt update
  sudo apt install package_name
  ```
- `dnf` or `yum`: Package managers for Red Hat-based systems.
  ```bash
  sudo dnf install package_name
  ```
- `pacman`: Package manager for Arch-based systems.
  ```bash
  sudo pacman -S package_name
  ```

## 7. Disk Management
- `df`: Display disk space usage.
  ```bash
  df -h
  ```
- `du`: Show directory or file size.
  ```bash
  du -sh folder_name
  ```
- `mount` and `umount`: Mount and unmount filesystems.
  ```bash
  sudo mount /dev/sdX /mnt
  sudo umount /mnt
  ```

## 8. System Monitoring
- `uptime`: Show system uptime.
  ```bash
  uptime
  ```
- `free`: Display memory usage.
  ```bash
  free -h
  ```
- `dmesg`: Print system messages.
  ```bash
  dmesg | tail
  ```

## 9. Searching and Filtering
- `grep`: Search for patterns in files.
  ```bash
  grep "pattern" file.txt
  ```
- `find`: Search for files and directories.
  ```bash
  find /path -name "file.txt"
  ```
- `awk` and `sed`: Text processing tools.
  ```bash
  awk '{print $1}' file.txt
  sed 's/old/new/g' file.txt
  ```

## 10. Archiving and Compression
- `tar`: Archive files.
  ```bash
  tar -cvf archive.tar folder_name
  ```
- `gzip` and `gunzip`: Compress and decompress files.
  ```bash
  gzip file.txt
  gunzip file.txt.gz
  ```
- `zip` and `unzip`: Create and extract zip files.
  ```bash
  zip archive.zip file.txt
  unzip archive.zip
  ```

---

Mastering these commands will significantly enhance your productivity and confidence in using Linux. Practice regularly to build fluency.