# Linux Commands

## File systems & Files

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

## xargs

- `ls | xargs echo'`
    - translates to `echo file1 file2 file3`
    - command is executed once with multiple arguments
- `ls | xargs -I@ echo @`
    - translates to `echo file1; echo file2; echo file3`
    - command is executed multiple times with one argument
- similar to ^^ but with reading from a file
    - `xargs echo < my_file`
    - `xargs -I@ echo @ < my_file`

## find

- `find ~ -type f -name itertools.py`

## Globbing

- `echo my_file{001..100}.txt` - 100 files with leading zeros

## Modify system firewall

```
$ iptables -I INPUT 5 -p tcp --dport 8969 -j ACCEPT
$ iptables -nL --line-numbers
```

## Port tunnelling

```
# socat tcp-listen:8969,reuseaddr,fork tcp:vm-jverner:8969
```

## sed

- "grep" between lines - `sed -n '/BEGIN task-2651/,/FINISH task-2651/p' the_file`

## clipboard

- `clipcopy` - copy to clipboard
  - `foo | clipcopy
- `clippaste` - paste from clipboard