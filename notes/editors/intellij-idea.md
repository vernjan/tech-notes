# IntelliJ IDEA

- see [IntelliJIDEA_ReferenceCard.pdf](https://resources.jetbrains.com/storage/products/intellij-idea/docs/IntelliJIDEA_ReferenceCard.pdf)

## General

- `ctrl + alt + s` - open Preferences (`cmd + ,`)
- `ctrl + alt + shift + s` - open Project structure (`cmd + ;`)
- `alt + f1` - select current file or symbol in any view ⚡
- `alt + home` - jump to navigation bar
- `ctrl + shift + f12` - maximize editor (`cmd + shift + f12`)
- ```ctrl + ` ``` - switch theme, keymap, view mode, ...

### Tabs & Windows

- `ctrl + tab` - tab & tool switcher ⚡
- `ctrl + alt + ]/[` - switch to previous/next IntelliJ IDEA window (`-`) ⚡
- `alt + left/right` - go to previous/next tab (`ctrl + left/right`) ⚡
- `f12` - go to previous tool window ⚡
- `escape` - go to editor (from tool window) ✔
- `shift + escape` - hide active (or last active) window ✔
- `ctrl + f4` - close active tab (`cmd + w`) ✔
- `alt + close tab (click X)` - close all tabs except the active one
- `ctrl + alt + shift UP/DOWN/LEFT/RIGHT` - resize tool windows

### Tool windows

- `alt + 0` - commit (`cmd + 0`) ✔
- `alt + 1` - project (`cmd + 1`) ✔
    - `shift + enter` - open in right split
    - `ctrl + d` - compare (`cmd + d`) ✔
- `alt + 2` - favorites (`cmd + 2`)
- `alt + 3` - find (`cmd + 3`)
- `alt + 4` - run (`cmd + 4`)
- `alt + 5` - debug (`cmd + 5`)
- `alt + 6` - problems (`cmd + 6`)
    - `alt + shift + i` - inspect current file ⚡
- `alt + 7` - structure (`cmd + 7`) ✔
- `alt + 8` - services (`cmd + 8`)
- `alt + 9` - Git (`cmd + 9`) ✔

### New files

- `alt + insert` - new file, source, diagram, ...  (`cmd + n`)
- `ctrl + alt + shift + insert` - new scratch file (`cmd + shift + n`)

## Edit

### Text selection

- `ctrl + w` - extend selection (`alt + up`) ✔
- `ctrl + shift + w` - shrink selection (`alt + down`) ✔
- `ctrl + shift + [ / ]` - select till code block start/end ⚡
- `alt + mouse drag` - column (rectangular) select ⚡
- `alt + shift + insert` - column selection mode (`cmd + shift + 8`) ✔

### Text manipulation

- `ctrl + d` - duplicate line (`cmd + d`) ✔
- `ctrl + y` - delete line (`cmd + backspace`) ✔
- `ctrl + shift + j` - join lines ✔
- `shift + enter` - start new line (the current line remains unchanged) ✔
- `ctrl + enter` - new line, don't move the cursor (`cmd + enter`)
- `ctrl + backspace/delete` - delete to word start/end ⚡
- `ctrl + shift + backspace/delete` - delete to line start/end ⭐
- `alt + shift + up/down` - swap lines ✔
- `ctrl + shift + up/down` - swap methods/blocks (`cmd + shift + up/down`) ✔
- `ctrl + c` - copy line (`cmd + c`) ✔
- `ctrl + x` - cut line (`cmd + x`) ✔
- `ctrl + shift + v` - paste from recent buffers ("local clipboard history") (`cmd + shift + v`)
- `ctrl + shift + u` - toggle word (selected block) case (`cmd + shift + u`) ✔

### Multi-cursors

- `alt + shift + click` - add new cursor ⚡
- `alt + shift + drag` - multi-select
- `ctrl, ctrl + UP/DOWN` - clone cursor up/down
- `alt + shift + g` - move all cursors to line ends ⚡
- `alt + j` - one by one select occurrences of the current word and add cursor (`ctrl + g`) ⚡
- `ctrl + alt + shift + j` - select all occurrences of the current word and add cursors (`ctrl + cmd + g`) ⚡

## Code

- `alt + enter` - show intention actions and quick-fixes ✔
- `alt + insert` - generate code (`cmd + n`) ⚡
- `ctrl + o` - override methods
- `ctrl + i` - implement methods
- `ctrl + alt + t` - surround with (if, else, try, catch, ...) (`cmd + alt + t`) ⚡
- `ctrl + alt + l` - reformat code (`cmd + alt + l`) ✔
- `ctrl + alt + o` - optimize imports (`ctrl + alt + o`) ✔
- `ctrl + alt + i` - auto-indent line(s) (`ctrl + alt + i`)
- `ctrl + /` - comment / uncomment with line comment (`cmd + /`) ✔
- `ctrl + shift + /` - comment / uncomment with block comment (`cmd + alt + /`) ✔

### Code completion

- `ctrl + space` - basic code completion ✔
- `ctrl + shift + space` - smart code completion
    - `enter` - insert
    - `tab` - replace
- `ctrl + shift + enter` - complete statement (`cmd + shift + enter`) ⚡
- `alt + /` - hippie completion

### Context info

- `ctrl + p` - parameter info (`cmd + p`) ⚡
- `ctrl + mouse` - brief info, resolves `var` type (`cmd + mouse`) ✔
- `ctrl + q` - quick documentation lookup (`ctrl + j`, `F1`)
- `alt + q` - context info (current method, class) (`ctrl + shift + q`)
- `ctrl + shift + p` - expression type info ⚡
- `ctrl + shift + i` - quick definition (`alt + space`)
- `ctrl + F1` - show descriptions of error or warning at caret (`cmd + F1`)
    - `alt + shift + enter` - apply suggested fix

## Live templates

- `ctrl + j` - live templates (`cmd + j`) ⚡
    - `fori` - for loop (use `tab` to complete all live templates)
    - `ifn` - if null
    - `inn` - if not null
    - `thr` - `throw new`
    - `souf` - `System.out.printf("");`
    - `sout` - `System.out.println();`
    - `soutm` - print method name
    - `soutp` - print method params
    - `soutv` - print (last) value

## Navigation

- `ctrl + b / ctrl + click` - go to declaration ✔
- `ctrl + shift + b` - go to type declaration ⚡
- `ctrl + alt + b` - go to implementations (`cmd + shift + b`) ⚡
- `ctrl + u` - go to super class/method (`cmd + u`) ⚡
- `ctrl + shift + t` - switch between class and test class (`shift + cmd + t`) ✔
- `ctrl + g` - go to line (`cmd + l`) ✔
- `alt + up/down` - go to previous/next method (`ctrl + [/]`) ⚡
- `ctrl + [/]` - move to code block start/end (`cmd + alt + [/]`) ⚡
- `ctrk + shift + m` - toggle code block start/end (`ctrl + m`) ⚡
- `f2 / shift + f2` - next/previous highlighted error
- `alt + space` - quick definition lookup
- `ctrl + +/-` - expand/collapse block ⚡
- `ctrl + shift + +/-` - expand/collapse all

### Recent locations & changes

- `ctrl + alt + left/right` - navigate back/forward (`cmd + alt + left/right`) ✔
- `ctrl + shift + backspace` - navigate to last edit location (`cmd + shift + backspace`) ⚡
- `ctrl + e` - recent files popup (`cmd + e`) ⚡
    - `ctrl + e` - recent edited files
- `ctrl + shift + e` - recent locations popup (`cmd + shift + e`) ⚡
    - `ctrl + shift + e` recent edited locations
- `ctrl + shift + k` - view recent changes (`alt + shift + c`)

### Usage search

- `alt + f7` - find usages (tool window) ✔
- `ctrl + f7` - highlight usages in file (`cmd + f7`) ⚡
- `ctrl + alt + f7` - show usages in file (popup) (`cmd + alt + f7`)

### Bookmarks ⚡

- `f11` - toggle bookmark (`f3`)
- `ctrl + f11` - toggle bookmark with mnemonic (`alt + f3`)
- `shift + f11` - show bookmarks (`cmd + f3`)
- `ctrl + 0-9` - go to bookmark

### Hierarchies

- `ctrl + f12` - file structure popup (`cmd + f12`) ✔
- `ctrl + h` - type hierarchy
- `ctrl + shift + h` - method hierarchy (`cmd + shift + h`)
- `ctrl + alt + h` - call hierarchy ✔

## Search & Replace

- `shift & shift` - search everywhere ✔
    - `/` - limit search for commands
    - `/url/` - limit search for URL mappings (web endpoints) ⚡
- `ctrl + n` - search class (`cmd + o`) ✔
- `ctrl + shift + n` - search file (`cmd + shift + o`) ✔
- `ctrl + alt + shift + n` - search symbol (`cmd + alt + o`)
- `ctrl + shift + a` - search action (`cmd + shift + a`) ✔

### Fulltext

- `ctrl + f` - find (`cmd + f`) ✔
- `ctrl + r` - replace (`cmd + r`) ✔
- `ctrl + shift + f` - global search (`cmd + shift + f`) ✔
- `ctrl + shift + r` - global replace (`cmd + shift + r`) ✔
- `f3` - find next (`cmd + g`) ✔
- `shift + f3` - find previous (`cmd + shift + g`) ✔

## VCS (Git)

- `ctrl + k` - commit (focus on commit message) (`cmd + k`) ✔
    - `ctrl + m` - commit message history (`ctrl + m`)
- `alt + 0` - commit (focus on changed files) (`cmd + 0`) ✔
- `ctrl + alt + z` - rollback changes (`cmd + alt + z`)
- `ctrl + shift + k` - push commits (`shift + cmd + k`)
- `ctrl + t` - update project (pull) (`cmd + t`) ✔
- ```alt + ` ``` - quick popup (`ctrl + v`) ⚡
- ```ctrl + shift + ` ``` - branches (`-`) ⚡

## Refactoring

- `ctrl + alt + shift + t` - refactor this (`ctrl + t`)
- `f5` - copy
- `f6` - move
- `shift + f6` - rename ✔
- `ctrl + f6` - change signature (`cmd + f6`) ✔

### Extracts

- `ctrl + alt + n` - inline (`cmd + alt + n`) ✔
- `ctrl + alt + m` - extract method (`cmd + alt + m`) ✔
- `ctrl + alt + v` - extract variable (`cmd + alt + v`) ✔
- `ctrl + alt + c` - extract constant (`cmd + alt + c`) ✔
- `ctrl + alt + f` - extract field (`cmd + alt + f`) ✔
- `ctrl + alt + p` - extract parameter (`cmd + alt + p`) ✔

## Compile & Run

- `ctrl + f9` - build project (`cmd + f9`)
- `ctrl & ctrl` - run anything
- `shift + f10/f9` - run/debug (`ctrl + r/d`)
- `ctrl + shift + f10/f9` - run/debug the current class/ test method (`ctrl + shift + r/d`)
- `alt + shift + f10/f9` - open run/debug dialog (`ctrl + alt + r/d`)

## Debugging

- `f7` - step into ✔
- `f8` - step over ✔
- `shift + f8` - step out
- `f9` - resume (`cmd + r`)
- `alt + f8` - evaluate expression ✔
- `alt + f9` - run to cursor
- `ctrl + f8` - toggle breakpoint (`cmd + f8`)
- `ctrl + shift + f8` - view breakpoints (`cmd + shift + f8`)

## Diagrams

`ctrl + alt + shift + d` - VCS local changes
`ctrl + alt + shift + u` - UML class diagram (invoke on package)

## GitHub Copilot

- `alt + [` - previous suggestion
- `alt + ]` - next suggestion
- `alt + \` - show all suggestions
- `tab` - accept full suggestion
- `ctrl + alt + RIGHT` - accept line
- `ctrl + RIGHT` - accept word
