# Linux

- [Linux commands](linux-commands.md)
- [Terminal shortcuts](terminal-shortcuts.md)
- [Terminator shortcuts](terminator-shortcuts.md)
- [Midnight Commander](mc.md)
- [less](less.md)
- [Zsh](zsh.md)
- [Disks & partitions](disks-partitions.md)

## Source

- [Explanation of “Everything is a File” and Types of Files in Linux](https://www.tecmint.com/explanation-of-everything-is-a-file-and-types-of-files-in-linux/) (Tecmint blog)

## File types

- **normal**
- **directories**
- **soft links** - shortcut to a file or directory
- **hard links** - additional name for an existing file (not directory)
- **socket** - pass data between 2 processes, possibly on different machines
- **named pipe** - connects output of P1 to input of P2 (`mkfifo NAME`)
- **character device** - device files that provide unbuffered serial access (one character at a time)
- **block device** - device files that provide buffered access to system hardware components

### Soft vs. hard links

- **soft link** - `ln -s SOURCE TARGET`
- **hard link** - `ln SOURCE TARGET`
- hard link is just a different name (same _inode_) while sof link is a new reference (alternative path) to the original file
- hard links are limited to same partitions
- removing a hard link causes no issues - inode has a counter of hard links, and it's not deleted until it reaches 0

## Partitions & mounts

- limited to 4 primary partitions - _extended_ partition as a workaround (servers as a container for more partitions)
- `lsblk` - list all devices
- `fdisk` - manage all around partitions
    - `fdisk -l` - list all partitions
    - `fdisk /dev/sdx` - manage partitions on the given disk
- `mkfs -v -t ext4 /dev/dsx` - make filesystem
- `mount` - list all mounts
    - `mount -v -t ext4 /dev/sdx /mnt/foo`
- `/etc/fstab` - permanent mounts

## Login shell

- **non-login shell** - does not read, and execute, the contents of `/etc/profile` or `.bash_profile files`,
  but rather reads, and executes, the `.bashrc` file instead.