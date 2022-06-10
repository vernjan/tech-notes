# GDB

- https://darkdust.net/files/GDB%20Cheat%20Sheet.pdf
- https://visualgdb.com/gdbreference/commands/

## Breakpoints

- `b/break main` - set break point at `main` function
- `b *main+20`

## Running

- `r/run` - run the binary
- `r < FILE` - run the binary, read from file
- `kill` - kill the running program

## Stepping

- `s/step` - do one step (dive into functions)
    - `si` - step instruction
- `n/next` - do one step (skip functions)
    - `ni` - next instruction
- `finish` - continue until the current function returns
- `c/continue` - continue execution

## Variables and memory

- `p[rint]/format [something]` - print value of  _something_
- `display/format [something]` - print value of _something_ after each step
- `x/format [something]` - print memory

### Something

- variable
  - `x argc`
  - `p *var` to dereference pointers 
- function - `x main`
- address - `x 0x804b170`
- register - `x $esp`

### Format

`ntu`
- `n` - number - how many
- `t` - type (`b` byte, `h` half-word, `w` word, `g` double-word)
- `u` - unit (`d` - integer, `s` - C string, `x` - hex, ...)

## Info

- `i/info *`
    - `i args` - argument variables of current stack frame
    - `i locals` - local variables of current stack frame  
    - `i functions` - all function names
    - `info proc mappings` - mapped address space

# GEF

https://gef.readthedocs.io/en/master/

- `checksec` - print which security protections are enabled in a binary
- `vmmap` - display memory space mapping  
- `got` - print _Global offset table_
- `aslr [on/off]` - turn on/off ASLR
