# bootleg cart notes

Notes and ROM dumps from multicart bootleg Game Boy carts.

The dumper used is insideGadgets GBxCart RW v1.2b. The modified dumper code can be found at [my fork](https://github.com/chfoo/GBxCart-RW/tree/multicart).

Work in progress.

## 108-in-1

* $FF82 is the cursor 1-based index

When cart is boot up:

* Write $AA to $5000
* Write $00 to $4000
* Write $01 to $2100

When game 1 (Pokemon Gold) is selected:

* Write $01 to $2100
* Write $E0 to $7BE0
* Write $BB to $5000
* Write $00 to $4000
* Write $20 to $7B20
* Write $55 to $5000
* Write $82 to $7B82
* Jump to $0100

### Game 1

`POKEMON_GOLD_US.gb`

* MD5: 02106d5967cff46f4862add4fdbeb5cb
* SHA1: 1e739723fbcf4dd7e7d62c1b5143695a29af5dd3

## 2-in-1 Pokémon Gold and Silver

* $c014 is the menu cursor's 0-based index
* When a choice is selected, code at ROM3f:6774 is copied to work ram D000 and run

Pseudocode (translated by Pikalax, thanks!):

```
Switch to ROM bank 1
Map some cartridge feature to SRAM
Read byte at [cd00+[c014]] to reg_a (inefficiently, i might add)
if reg_a != 0:
  write reg_a to [a000]
  write [cd0a+[c014]] to [a000]
  write [cd1e+[c014]] to [b000]
  write [cd28+[c014]] to [a000]
  restore hardware ident from [fff0]
  jump to Boot
else:
  write reg_a to [a000]
  write [cd0a+[c014]] to [a000]
  write [cd1e+[c014]] to [b000]
  write [cd28+[c014]] to [a000]
  restore hardware ident from [fff0]
  jump to code at 00:05C5
```

WIP
