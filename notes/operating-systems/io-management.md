# I/O Management
- **IN** - mouse, keyboard, microphone
- **OUT** - display, speakers
- **BOTH** - disk, network, flash drives
- devices also have microcontrollers (CPUs) and memory
- PCI (Peripheral Component Interconnect) / **PCIe**
- pseudo (virtual) devices
    - `/dev/null`, `/dev/random`
- **call path** - user process --> (system call) kernel --> driver --> device
- sync vs. async operations

## CPU-device interactions
- **memory-mapped IO**
    - some parts of RAM are dedicated for device registrations
- **IO port** (direct)
    - special instructions targeting the device register
    - system call `ioctl(fd, request)`
- interrupts vs. polling (tradeoffs)

## Device drivers
- per device type
- provided by hardware manufacturers
- OS offers a framework (interface) for drivers
- block (disks) / character (keyboard) / network devices
- represented as a special device _files_ in `/dev`

## Block device stack
- unit of abstraction = **file**
- kernel file system
    - where is the file (physically)
    - permissions check
- POSIX API - many implementations

## Virtual file system (VFS)
- sits between the kernel and a concrete file system (i.e. concrete file systems implement a kernel API)
- transparent layer which abstracts
    - multiple disks
    - networks disks
    - different file systems implementations
- **file descriptor** - how OS sees a file (remember that almost everything is a file in Linux)
- **dentry** - directory entry
- **block types**
    - data blocks
    - inode blocks
    - free blocks
- **superblock** maps (using multiple bitmaps) which block is data/inode/free
- `stat FILE` - show detailed file info

### inode
- persistent representation of a file
- **metadata** - filename, size (block count), owner, permissions
    - **timestamps**
        - **access**
        - **change** - changes to inode (rename, update permissions, ..)
        - **modify** - modify data
- index of all file data blocks
    - direct pointers
    - indirect pointers - point to block of pointers
    - double indirect pointers - point to block of pointers of pointers
        - allows to handle large files