# Vim - Command mode

- `ctrl+d` - list completion options
- `tab` - completion

## Commands
- `:q[!]` - (force) quit
- `:w [FILENAME]` - save (write) the file
- `:wqa` - save (write) and quit all buffers
- `:x, ZZ` - save the file and exit
- `:r <FILENAME>` - read an external file into this file
- `:<NUMBER>` - go to line number
- `:ter` - terminal

### External commands
- `:!<COMMAND>` - execute external command (e.g. `:!ls`)
- `:r !<COMMAND>` - read external command output into this file (e.g. `:r !ls`)
