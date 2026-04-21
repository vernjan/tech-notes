# Unicode

- Unicode is a standard for encoding characters from all writing systems, symbols, and emojis
- It assigns a unique **code point** (a 32-bit number) to each character
- Can represent over 1 million characters in various encoding forms like UTF-8, UTF-16, and UTF-32.
    - 11 of the 32 bits are always zero

## UTF-8

- The most common encoding form, using 1 to 4 bytes per character
- ASCII characters (code points 0-127) are represented in a single byte
- Non-ASCII characters use multiple bytes, with the first byte indicating how many bytes follow
- Allows to look at any byte in a sequence and tell if you are at the start of a UTF-8 sequence or somewhere in the middle