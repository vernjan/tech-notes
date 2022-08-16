# Storage

## Sources
- [direct-attached storage (DAS)](https://www.techtarget.com/searchstorage/definition/direct-attached-storage)
- [network-attached storage (NAS)](https://www.techtarget.com/searchstorage/definition/network-attached-storage)
- [What is a SAN? Ultimate storage area network guide](https://www.techtarget.com/searchstorage/definition/storage-area-network-SAN)

## Block, file, object
- **block storage** - sequence of bytes, most low level
    - common API - **SCSI**
    - transports - SAS (serial attached SCSI), FCP, iSCSI
    - API - `read/write(disk, offset, data)`
- **file storage** - manages data as a file hierarchy (on top of a block storage)
    - access via Samba, NFS
- **object/blob** - manages data as objects
    - object - data, metadata, UUID
    - access via HTTP, ...
    - AWS S3

## DAS, NAS, SAN

### DAS (direct-attached storage)
- attached directly to a computer without going through a network
- only the host computer can access the data directly
- other devices must go through the host computer to work with the data
- connected via SCSI, SATA, PCIe, ...

### NAS (network-attached storage)
- accessed via Ethernet (LAN), the network is shared for all workloads
    - protocols NFS or SMB
    - NAS implements a file system
- independent network node, has its own IP address
- implements a file system and is accessed via NFS or SMB
- enables multiple users and heterogeneous client devices to retrieve data from centralized disk capacity
- usually handles _unstructured_ data (audio, video, images, ...)
- can support additional features such as backups, remote management, ...

### SAN (storage area network)
- **tldr** - a network of disks with unified access and central management
- high-speed network that interconnects and exposes a shared pool of storage devices
    - **physical** - storage array
    - **virtual** - VMWare vSAN
- layers
    - **host layer** - servers running the workloads (such as DBs or VMs)
        - they have dedicated network adapters for SAN network - **HBA** - host bus adapter
    - **fabric layer** - cabling and network devices interconnecting SAN hosts and SAN storage
    - **storage layer** - disks, SSDs, ..
        - typically organized into physical RAID groups
- **protocols**
    - **FCP** (fibre channel protocol) - maps SCSI commands over fibre channels
    - **iSCSI** - maps SCSI commands over TCP/IP
- highly scalable, centrally managed
- usually handles _structured_ data (a block storage for DBs or VMs)
- redundancy
    - hosts have usually 2 HBAs
    - network has at least 2 switches
    - storage array has multiple ports and disks in RAID
- data deduplication, encryption

## SCSI, NVMe

### SCSI (small computer system interface)
- block storage API
- client-server protocol5
- **commands** - read/write, copy, zero, ...
- **command structure**
    - initiator ID
    - target ID
    - LUN - logical unit number - identifies one of the disks behind SCSI
    - tag
    - CDB - command descriptor block
- **sector** - 512 bytes
- supports **task management** - each LU keeps a task queue
    - `TASK_ABORT` - abort task(s) by _tag_
    - `LUN_RESET` - abort all tasks
- supports **exceptions and errors**

### NVMe (non-volatile memory express)
- communication protocol - modern alternative to AHCI (SCSI)
- built for SSDs (flash) - SCSI was designed for HDD and is not effective for fast SSDs
    - uses parallel access (impossible for rotating disks)
- supports PCIe

## HDD, SSD
- **HDD**
    - equally fast reads and writes
    - don't wear out
    - sequential access - data locality matters
- **SSD**
    - reads faster than writes
    - limited number of overwrites
    - random access - possibly parallel
    - consume less power

## M.2
- physical slot (connector)
- replaces `mSATA`
- can also be used for WiFi, BT, NFC, ..
- supports PCIe, SATA III, USB 3.0
- **PCIe + NVMe** - fastest connections for SSDs

## RAID
- `0` - join disks together - increased capacity but no redundancy
- `1` - mirroring, requires double capacity
- `5` - single parity, at least 3 disks, 1 can fail
- `6` - double parity, at least 4 disks, 2 can fail
