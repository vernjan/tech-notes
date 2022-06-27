# I/O Management
- IN: mouse, keyboard, microphone
- OUT: display, speakers
- BOTH: disk, network, flash drives
- devices also have microcontrollers (CPUs) and memory
- PCI (Peripheral Component Interconnect) / PCIe
- pseudo (virtual) devices
    - `/dev/null`, `/dev/random`
- user process -> (system call) kernel -> driver -> device
- sync vs. async operations

## CPU-device interactions
- **memory-mapped IO**
    - some parts of RAM are dedicated for device registrations
- **IO port** (direct)
    - special instructions targeting the device registry
    - `ioctl(fd, request)` system call
- interrupts or polling (tradeoffs)

## Device drivers
- per device type
- provided by HW manufacturers
- OS offers a framework (interface) for drivers
- block (disks) / character (keyboard) / network devices
- represented as a special device _file_
- `/dev`, `tmpfs` (file system which keeps all of its files in virtual memory), `devfs`

## Block device stack
- unit of abstraction = **file**
- kernel file system
    - where is the file (physically)
    - permissions check
- POSIX API - many implementations 