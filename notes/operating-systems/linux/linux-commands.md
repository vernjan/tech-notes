# Linux Commands

## Files

- `du -sh *` - **disk usage**
    - `-s` - summary of this dir
    - `-s *` - summary of all files in this dir
    - `-h` - human-readable
- `df` - **disk free** - print all filesystems
    - `df .` - current filesystem
    - `df PATH` - filesystem for the given path
    - `-h` - human-readable
- `stat`
- `debugfs` - debugging/inspecting filesystem internals
    - `open FS_NAME`

## dpkg

- `dpkg -i PACKAGE` - install (DEB) package
- `dpkg -s/--status PACKAGE` - show package info
- `dpkg -l/--list [pattern]` - show package info

## su

- `su - [user]` - `-` mean to use a _login shell_

## ss

- `-plt` - process, listen, full TCP

## Modify system firewall

```
$ iptables -I INPUT 5 -p tcp --dport 8969 -j ACCEPT
$ iptables -nL --line-numbers
```