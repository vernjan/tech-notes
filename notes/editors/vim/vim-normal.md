# Vim - Normal mode

## Navigation
- `h, j, k, l`  - left, down, up, right
- `w, W` - next word/WORD*
- `e, E` - end of this or next word/WORD*
- `b, B` - beginning of this or previous word/WORD*
- `ge, gE` - end of previous word/WORD*
- `0` - start of line
- `^` - start of line after whitespaces
- `$` - end of line
- `%` - matching bracket (`(), [], {}`)
- `*, #` - next (previous) occurrence of this word
- `), (` - next (previous) sentence
- `}, {` - next (previous) paragraph (empty line)
- `f<CHARACTER>, F<CHARACTER>` - _find_ - next/previous character on this line
- `t<CHARACTER>, T<CHARACTER>` - _till_ - before next/previous character on this line
- `;` - repeat last `f,F,t,T` movement
- `,` - repeat last `f,F,t,T` movement backwards
- `<NUMBER>|` - jump to column

### *word vs. WORD
_This is mind-blowing example!_
- **words** - `This`, `is`, `mind`, `-`, `blowing`, `example`, `!`
- **WORDS** - Separated by whitespaces: `This`, `is`, `mind-blowing`, `example!`

### Advanced Navigation
- `]m, [m` - next (previous) start of method (_coding_)
- `]M, [M` - next (previous) end of method (_coding_)
- `]), [(` - closing `)` / opening `(` (from the inside of the block)
- `]}, [{` - closing `}` / opening `{` (from the inside of the block)
- `gd` - go to variable/method declaration (_coding_)

## Jumps & Scrolling
- `gg` - go to the first line
- `G` - go to the last line
- `<NUMBER>G,<NUMBER>gg` - go to line number
- `H, M, L` - jump to screen position without scrolling (high, middle, low)
- `ctrl+d, ctrl+u` - jump half screen down/up
- `ctrl+f, ctrl+b` - jump full screen front/back
- `ctrl+e, ctrl+y` - scroll one line down/up
- `zt, zb, zz` - scroll top, bottom, middle (cursor does not move)

## Text Manipulation
- `x, X` - delete, backspace
- `r` - replace single character (`R` enters _replace_ mode)
- `d<MOVE>` - deletion
    - `dw` - delete word
    - `d2W` - delete 2 WORDS
    - `dt"` - delete till `"`
    - `dd` - delete line
    - `d$, D` - delete until the end of this line
- `c<MOVE>` - change (delete and enter _insert_ mode)
    - `c$, C` - change until the end of this line
- `s` - substitute (delete character and enter _insert_ mode)
    - `[COUNT]s` - substitute x characters
- `S, cc` - substitute line (delete line and enter _insert_ mode)
- `.` - repeat the last manipulation command
- `~` - toggle case (upper/lower) of this character or marked text
- `g~<MOVE>` - toggle case (upper/lower)
- `gu<MOVE>, gU<MOVE>` - change case to lower/upper
- `J` - join lines
- `>>, <<` - indent/unindent line


