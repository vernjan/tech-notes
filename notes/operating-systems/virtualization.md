# Virtualization
- allow concurrent execution of multiple OSs on the same physical machine
- **hypervisor** - virtualization layer sitting between HW and VMs
    - also called **VMM** - Virtual Machine Monitor
    - transparent to VM
    - in control of system resources
- **full virtualization** - guest OS runs without any modifications
    - could negatively impact performance (need for binary translation of some instructions)
    - **paravirtualization** - guest OS is modified to run faster with a hypervisor

## Models
- **bare-metal** (hypervisor based)
    - type 1
    - Citrix XenServer, VMWare ESX, Microsoft Hyper-V
- **hosted**
    - type 2
    - instead of the standard hypervisor there is a host OS with "hypervisor" module
    - host OS owns all HW
    - KVM, VirtualBox, VMWare Player

## Hardware protection levels
- x86 - 4 rings
    - **ring 0** - the highest privileges - hypervisor or OS
    - **ring 3** - apps
    - root mode vs non-root mode
- **non-privileged operations** are executed directly on HW - fast
- **privileged operations** - CPU causes a trap to hypervisor
    - illegal -terminate VM
    - legal - hypervisor emulates the expected HW behavior

## Hardware features (x86)
- **root** (host) and **non-root** (guest) mode
- improved instruction set
- faster switches between VMs (support in page tables and TLB)

## Memory virtualization
- **virtual**
- **physical** - what guest OS think is real HW
- **machine** - real HW

## Device virtualization
- high diversity of devices
- **models**
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