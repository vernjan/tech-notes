# Linux Commands

## du & df
- `du -sh *` - disk usage
  - `-s` - summary of this dir
  - `-s *` - summary of all files in this dir
  - `-h` - human-readable
- `df` - disk free - all filesystem
- `df .` - disk free - current filesystem

## dpkg
- `dpkg -i PACKAGE` - install (DEB) package
- `dpkg -s/--status PACKAGE` - show package info
- `dpkg -l/--list [pattern]` - show package info

## su
- `su - [user]` - `-` mean to use a _login shell_