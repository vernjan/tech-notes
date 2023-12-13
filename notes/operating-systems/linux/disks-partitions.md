# Disks & Partitions

- `/dev/sda` - SCSI disk
- `/dev/nvme0n1p1` - NVMe disk

## Logical volumes - device mapper

- LVM - [Logical Volume Manager](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux))
    - uses **device mapper**
- `dmsetup` - low level **logical** volume management
    - one logical volume can map onto multiple disks/partitions
- `dmsetup ls` - list all device mapper devices
- `/dev/mapper` - device mapper
- `/dev/dm-X` - device mapper partition

```
# lsblk 
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda           8:0    0   256G  0 disk 
├─sda1        8:1    0   600M  0 part /boot/efi
├─sda2        8:2    0     1G  0 part /boot
└─sda3        8:3    0 254.4G  0 part 
  ├─rl-root 253:0    0    70G  0 lvm  /
  ├─rl-swap 253:1    0  15.7G  0 lvm  [SWAP]
  └─rl-home 253:2    0 424.7G  0 lvm  /home
sdb           8:16   0   256G  0 disk 
└─sdb1        8:17   0   256G  0 part 
  └─rl-home 253:2    0 424.7G  0 lvm  /home
sr0          11:0    1  1024M  0 rom  
```

## Adding a new phyisical disk/partition

https://thelinuxcluster.com/2018/07/09/formatting-nvme-partition-on-centos-7/

```
# fdisk -l
# fidsk DEVICE  # e.g. /dev/sdb | /dev/nvme0n2
  n  # new partition
  p  # primary partition
  ..
  w  # write changes
# mkfs.ext4 DEVICE  # e.g. /dev/sdb1
# mkdir /media/nvme
# mount /dev/nvme0n1p1 /media/nvme
# blkid
# vim /etc/fstab
  UUID=nvme_UUID /media/nvme ext4 defaults 0 0
# chown -R user:usergroup /media/nvme
```
