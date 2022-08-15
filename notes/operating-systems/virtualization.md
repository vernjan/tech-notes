# Virtualization
- allow concurrent execution of multiple OSs on the same physical machine
- **hypervisor** - virtualization layer sitting between hardware and VMs
    - also called **VMM** - Virtual Machine Monitor
    - transparent to VM
    - in control of system resources
- **full virtualization** - guest OS runs without any modifications
    - could negatively impact performance (need for binary translation of some instructions)
- **paravirtualization** - guest OS is modified to run faster with a hypervisor

## Models
- **bare-metal / native** (hypervisor based)
    - type 1
    - Citrix XenServer, VMWare ESX, Microsoft Hyper-V
- **hosted**
    - type 2
    - instead of the standard hypervisor there is a host OS with "hypervisor" module
    - host OS owns all hardware
    - KVM, VirtualBox, VMWare Player

## Hardware protection levels
- x86 - 4 rings
    - **ring 0** - the highest privileges - hypervisor or OS
    - **ring 3** - apps
- **root mode** (host) vs. **non-root mode** (guest)
- **non-privileged operations** are executed directly on hardware - fast
- **privileged operations** - CPU causes a trap to hypervisor
    - illegal - terminate VM
    - legal - hypervisor emulates the expected hardware behavior

## Memory virtualization
- **virtual** - same
- **physical** - what guest OS thinks is real hardware
- **machine** - real hardware

## Device virtualization
- high diversity of devices
- **pass-trough model**
    - exclusive, potentially direct access (hypervisor bypass)
    - troublesome sharing and migration
- **hypervisor direct model**
    - all calls to devices intercepted by hypervisor
    - guest VM decoupled from the concrete device
    - adds latency
- **split-device driver model**
    - front-end and back-end driver
    - paravirtualization only