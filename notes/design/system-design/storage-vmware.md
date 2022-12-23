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
- **Protocol Endpoint** (PE) - volume of 0 capacity, a proxy for I/O
    - PE is the only connected volume to ESXi (e.g. LUN 255)
    - PE can connect up to 16k sub-LUNs (i.e. up to 16k virtual volumes), e.g. `255:6`, `255:7`, ..
    - vVols are connected to the PE only if the VM is running
    - data path
    - backed by SCSI spec
        - Administrative Logical Unit (**ALU**) = PE
        - Subsidiary Logical Unit (**SLU**) = virtual volume
    - **vVol binding** - vVol (SLU) is bound to PE (ALU)
        - prerequisite for any IO between the VM and the volume
        - **out-of-band** - vSphere calls `bindVirtualVolume(vVolIds)`
            - VASA returns SLUs
            - host (ESXi) combines with ALU to get the full path
            - IO is ready (SCSI commands has both ALU:SLU)
        - **in-band bind** - via SCSI protocol to PE
            - binding is critical (no bind, no VM I/O)
            - faster, more reliable
            - the very first bind must go through VASA
            - PE can bind to another PE (redirecting traffic)
- **storage container** - SCSI, NVMe or NAS (just one)
    - name
    - max volume size
    - PE type
        - SCSI - PE = 0 capacity LU binding the virtual volumes
        - NVMe - doesn't need PE
- **VASA** - API implemented by a storage to enable the "control path" operations
    - create VM, replicate, migrate, take snapshot, ...
    - vSphere calls VASA