# How to Check Memory in Linux

This guide provides tips and commands to check memory usage and program memory details on Linux.

## 1. Check System Memory Information
- Use the `/proc/meminfo` file to view detailed memory statistics:
  ```bash
  cat /proc/meminfo
  ```
- This file provides information about total, free, and available memory, as well as swap usage.

## 2. Check Memory Usage of a Specific Process
- Use the `/proc/<PID>/status` file to view memory usage of a specific process:
  ```bash
  cat /proc/<PID>/status | grep -i vm
  ```
- Replace `<PID>` with the process ID of the program.

## 3. Monitor Memory in Real-Time
- Use the `top` or `htop` command to monitor memory usage in real-time:
  ```bash
  top
  ```
  or
  ```bash
  htop
  ```

## 4. Check Virtual Memory Maps of a Process
- Use the `/proc/<PID>/maps` file to view the memory layout of a process:
  ```bash
  cat /proc/<PID>/maps
  ```
- This shows the memory regions (stack, heap, text, etc.) used by the process.

## 5. Check Memory Usage with `free`
- Use the `free` command to get a summary of memory usage:
  ```bash
  free -h
  ```
- The `-h` flag displays the output in a human-readable format.

## 6. Inspect Memory with `pmap`
- Use the `pmap` command to display the memory map of a process:
  ```bash
  pmap <PID>
  ```
- Replace `<PID>` with the process ID.

## 7. Debug Memory with `gdb`
- Use `gdb` to inspect memory during program execution:
  ```bash
  gdb ./program
  (gdb) run
  (gdb) info proc mappings
  ```

## 8. Check Swap Usage
- Use the `swapon` command to check swap usage:
  ```bash
  swapon --show
  ```

## 9. Analyze Memory Leaks with `valgrind`
- Use `valgrind` to detect memory leaks in your program:
  ```bash
  valgrind --leak-check=full ./program
  ```

## Summary
These commands are essential for debugging, optimizing, and understanding memory usage in Linux systems. Use them to monitor system memory, analyze program memory, and debug memory-related issues effectively.