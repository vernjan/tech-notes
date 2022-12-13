# Storage - VMware

## VMFS

- filesystem for storing VMs - stored as a single volume on the storage array
- poor granularity, blackbox for storage admins
- file types
    - **VMX** - VM config file (OS type, disk sizes, networking, ...)
    - **VMDK** - VM disk
    - **NVRAM** - VM BIOS
    - **VMSN**, **VMSD** - VM snapshots

## vVols (virtual volumes)

- each VM has all of its volume stored as a separate volumes on the storage array
- granular - easy to apply different policies, take snapshots, do backups, ...
- opens the door for array based features
- ESXi limits
    - 512 devices or 2,000 logical path
- **Protocol Endpoint** (PE) - volume of 0 capacity, a proxy to virtual volumes
    - PE is the only connected volume to ESXi (e.g. LUN 255)
    - PE can connect up to 16k sub-LUNs (i.e. up to 16k virtual volumes), e.g. `255:6`, `255:7`, ..
    - vVols are connected to the PE only if the VM is running