# less

-`h` - help

## Movement

- `j / k` - line down / up (`5j` - 5 lines down)
- `d / u` - half page down / up
- `f / b` - page down (`space` also works) / up
- `g / G` - start / end of doc
- `NUMBER g` (`50g`) - go to line NUMBER
- `NUMBER p` (`50p`) - go to % NUMBER

## Cool tricks

- `=` or `ctrl + g` - status line
- `!` - execute shell
- `shift + F` - tailing (`ctrl + c` to stop)

## Changing settings

- `-KEY`
    - `-N` - show line numbers
    - `-i` - ignore case
    - `-g` - highlight search matches
    - `-W` - highlight unread

## Searching & filtering

- `/` - forward
- `?` - backward
- `&` - filter (even filtered view can be searched and tailed)
    - `ctrl + N or !` - **N**egative filter
    - `ctrl + R` - no **R**egulars
- `n / N` - search next / previous
- `ESC u` - toggle search highlight

## Marks

- `m LETTER` - mark current top line (on the screen)
- `M LETTER` - mark current bottom line (on the screen)
- `' LETTER` - go to mark