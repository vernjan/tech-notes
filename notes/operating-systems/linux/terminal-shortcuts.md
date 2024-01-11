# Terminal Shortcuts

## Navigation

- `ctrl + a` - jump to line start
- `ctrl + e` - jump to line end
- `ctrl + xx` - jump to line start, jump back to the original position
- `ctrl + LEFT/RIGHT` - jump by words

## Cut & paste

- `ctrl + w` - cut the word before cursor
- `alt + d` - cut the word after cursor
- `ctrl + u` - cut all before cursor
- `ctrl + k` - cut all after cursor
- `ctrl + y` - paste

## Editing

- `alt + t` - swap words
- `alt + .` - paste the last word from previous command

## Control

- `ctrl + l` - clear screen
- `ctrl + z` - send the currently running process into background
- `ctrl + d ` - exit the current shell
- `ctrl + c` - send `SIGINT`
- `ctrl + r` - search in history
- `ctrl + g` - exit history search
- `ctrl + s` - pause screen output
- `ctrl + q` - resume screen output

## Misc

- `ctrl + _` - undo
- `alt + r` - undo all changes to a command recalled from history
- `ctrl + x, ctrl + e` - edit the current command in `$EDITOR`
- `!!` - replaced with last command from history (for example `sudo !!`)
- `!n` - replaced with `n`-th command from history (for example `!3`)