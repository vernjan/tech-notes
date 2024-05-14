# Vim

- `:help [TOPIC]` - show help
- `ctrl+g` - show status bar (filename, total number of lines, ...)

## Modes

https://www.freecodecamp.org/news/vim-editor-modes-explained/

- [normal](vim-normal.md)
- [insert](vim-insert.md)
- [visual](vim-visual.md)
- [command](vim-command.md)
- replace - enter _replace_ mode with `R`

## Undo & Redo

- `u` - undo single change
- `U` - undo all changes on the same line
- `ctrl+r` - redo

## Copy & Paste

- `p, P` - paste after/before this line
- `ctrl+r <REGISTER_NAME>` - paste (in _insert_ mode)
- `y<MOVE>` - copy (yank)
- `Y, yy` - copy (yank) line

### Registers

_Whatever is deleted or copied (yanked) goes into registers._

- `:reg` - show registers
- `"<REGISTER_NAME>p` - paste from register
- `"<REGISTER_NAME>y` - copy into register
- `"<CAPITAL_REGISTER_NAME>y` - append into register

### Types of registers

_Line (l)_ vs. _Character (c)_

- `""` - default register
- `"0` - last yank
- `"1-9` - delete history
- `"a-z` - custom named registers
- `"-` - small register holds last _character-wise_ yank/delete
- `"_` - black hole register (like `/dev/null`)
- `"/` - last search register
- `"+` - system clipboard (ctrl+c)
- `"*` - system clipboard (mouse highlight)

## Window Management

- `:sp[lit], ctrl+w s` - split horizontally
- `:vsp[lit], ctrl+w v` - split vertically
- `ctrl+w q` - close window
- `ctrl+w h,j,k,l` - switch to window in direction
- `ctrl+w ctrl+w` - switch to the next window

## Buffers

- `:e FILENAME` - load (edit) file (creates new buffer)
- `:ls, :buffers` - list buffers
- `:b <NUMBER/NAME>` - switch to buffer by number/name
- `:bn, :bp` - switch to next/previous buffer
- `:b#` - switch to last buffer
- `:bd` - delete buffer

## Search

- `/pattern, ?pattern` - search forward/backward (supports _regex_)
    - `/pattern\c` - case in-sensitive
    - `/pattern\C` - case-sensitive
- `n, N` - next/previous search result
- `/ + enter, ? + enter` - repeat the last search

### Configuration

- `:set ic` - ignore case
- `:set hls` - highlight search results
- `:set is` - incremental search (jump immediately to results)

## Replace (Substitute)

https://linuxize.com/post/vim-find-replace/

```
:[range]s/{pattern}/{string}/[flags] [count]
```

- `:s/pattern/string` - replace (substitute) once on this line (use empty _string_ for deletion)
- `:%s/pattern/string` - replace once/all (depends on setting) in this buffer (file)
- `:#,#s/pattern/string` - replace in range
    - `:3,10s/foo/bar/g` - replace from 3rd to 10th line
    - `:.,$s/foo/bar/` - replace from the current line until the end of this buffer
    - `:.,+4s/foo/bar/g` - replace until 4 lines below the current line

### Flags

- `g` - global - replace all in the given context (line, range, buffer)
- `c` - ask for confirmation
- `i` - case in-sensitive
- `I` - case-sensitive

## Marks

- `m<NAME>` - create mark on this line
    - `name` - lowercase letter - local mark
    - `NAME` - uppercase letter - global mark
- ``` `<NAME> ``` - jump to mark
- `'<NAME>` - jump to start of the line with the mark
- `:marks` - list marks
- `:delm <NAMEs>` - delete marks
- `:delm!` - delete all local marks

## Jumps & Changes

- https://medium.com/breathe-publication/understanding-vims-jump-list-7e1bfc72cdf0
- https://medium.com/usevim/vim-101-the-jump-and-change-lists-ef15cfb22c30

- `:ju[mps]` - list all jumps
- `ctrl+i, ctrl+o` - jump forward/back
- ``` `` ``` - jump to last position
- ``` `. ``` - jump to last edit
- `:changes` - list of changes
- `[NUMBER]g;` - go to previous change (close changes list first)

## Text Objects

https://blog.carbonfive.com/vim-text-objects-the-definitive-guide/

```
[NUMBER][COMMAND]a/i[MOTION]
```

- `a` - around word (include surrounding whitespace)
- `i` - inner word (without whitespace)

### Motions

- `a/iw` - around/inner word
- `a/is` - around/inner sentence
- `a/ip` - around/inner paragraph
- `a/i",'` - around/inner `", '`
- `a/i{, [, (` - around/inner `{, [, (`

## Macros

- `q<NAME>` - record macro
- `q` - stop recording
- `@<NAME>` - play macro
- `@@` - re-run last macro

## Advanced moves

- `[count]` - repeat the following movement/command
    - `3w` - jump to 3rd word
    - `5j` - jump 5 lines down
    - `4/foo` - find the 4th foo
    - `2dd` - delete 2 lines
- `dt"` - delete till `"`
- `y2/foo` - copy (yank) till the second foo
- ``` y`a ``` - copy (yank) till mark `a`
- `vi"` - select text in `"` (See _Text objects_)
- `das` - delete this sentence
- `v.,/foo` - select text from the cursor to `foo`
- `ciw` - change this word
- `xp` - swap character

## Multiline inserts

- use **visual block mode** (`ctrl+v` or `ctrl+q`)
- https://stackoverflow.com/questions/9549729/vim-insert-the-same-characters-across-multiple-lines