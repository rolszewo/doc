- [Vim Registers](#vim-registers)
  - [types of registers](#types-of-registers)
    - [1. unnamed register `""`](#1-unnamed-register-)
    - [2. 10 numbered registers `"0` to `"9`](#2-10-numbered-registers-0-to-9)
    - [3. small delete register `"-`](#3-small-delete-register--)
    - [4. 26 named register `"a` to `"z` or `"A` to `"Z`](#4-26-named-register-a-to-z-or-a-to-z)
    - [5. 3 Read-only registers](#5-3-read-only-registers)
    - [6. alternate file register `"#`](#6-alternate-file-register-)
    - [7. expression register `"=`](#7-expression-register-)
    - [8. selection and drop registers `"*`, `"+` and `"~`](#8-selection-and-drop-registers---and-)
    - [9. black hole register `"_`](#9-black-hole-register-_)
    - [10. last search pattern register `"/`](#10-last-search-pattern-register-)
  - [working with registers](#working-with-registers)
    - [list the registers](#list-the-registers)
    - [use a register](#use-a-register)
      - [copy something into a register](#copy-something-into-a-register)
    - [paste something from a register](#paste-something-from-a-register)
      - [normal or visual mode](#normal-or-visual-mode)
      - [insert or command mode](#insert-or-command-mode)
      - [visual mode](#visual-mode)
    - [empty a register](#empty-a-register)
    - [delete a register](#delete-a-register)

# Vim Registers

## types of registers

There are ten types of registers:

### 1. unnamed register `""`

Vim fills this register with text deleted with the `d` `c`, `s`, `x` commands
or copied with the yank `y` command, regardless of whether or not a specific
register was used (e.g.  `"xdd`).  This is like the unnamed register is pointing to the last used register.  Thus when appending using an uppercase register
name, the unnamed register contains the same text as the named register.
An exception is the `"_` register: `"_dd` does not store the deleted text in any
register.
Vim uses the contents of the unnamed register for any put command (`p` or `P`)
which does not specify a register.  Additionally you can access it with the
name `""`.  This means you have to type two double quotes.  Writing to the `""`
register writes to register `"0`.

### 2. 10 numbered registers `"0` to `"9`

`"0` will always have the content of the latest yank, and the others will have last 9 deleted text.
Being `"1` the newest, and `"9` the oldest.
With each successive deletion or change, Vim shifts the previous contents
of register 1 into register 2, 2 into 3, and so forth, losing the previous
contents of register 9.
So if you yanked some text, you can always refer to it using `"0p`

### 3. small delete register `"-`

This register contains text from commands that delete less than one line,
except when the command specifies a register with e.g. `"x`.

### 4. 26 named register `"a` to `"z` or `"A` to `"Z`

Vim fills these registers only when you say so.  Specify them as lowercase
letters to replace their previous contents or as uppercase letters to append
to their previous contents.

### 5. 3 Read-only registers

- `.` Contains the last inserted text.
- `%` Contains the name of the current file.
- `:` Contains the most recent executed command-line.

### 6. alternate file register `"#`

Contains the name of the alternate file for the current window.

### 7. expression register `"=`

This is not really a register that stores text, but is a way to use an
expression in commands which use a register.  The expression register is
read-write.

### 8. selection and drop registers `"*`, `"+` and `"~`

Use these registers for storing and retrieving the selected text for the GUI.

### 9. black hole register `"_`

When writing to this register, nothing happens.  This can be used to delete
text without affecting the normal registers.  When reading from this register,
nothing is returned.

### 10. last search pattern register `"/`

Contains the most recent search-pattern. This is used for "n" and 'hlsearch'.

## working with registers

### list the registers

List all registers

```bash
:reg[ister]
```

List only register `a`

```bash
:reg[ister] a
```

List register `a` and `c`

```bash
:reg[ister] a c
```

### use a register

#### copy something into a register

**Copy the whole line to register s**

```bash
"sY
```

or

```bash
"syy
```

**Copy up to the end of the line to register s**

```bash
"sy$
```

**Copy up to the next o to register s

```bash
"sto
```

### paste something from a register

#### normal or visual mode

Paste content from register s**

```bash
"sp
```

Paste content from register s in line above

```bash
"sP
```

#### insert or command mode

Paste content from register s
`CTRL`-`R`+`s`

#### visual mode

When using a put command like `p` or `P` in Visual mode, Vim will try to replace the selected text with the contents of the register. The previously selected text is put in the unnamed register.  If you want to put the same text into a Visual selection several times you need to use another register.  E.g., yank the text to copy, visually select the text to replace and use `"0p`. You can repeat this as many times as you like, the unnamed register will be changed each time.

### empty a register

Delete the content of register s

type `q a q`

or

```bash
:let @s=''
```

### delete a register

Delete the register s

```bash
:call setreg('s',[])
```
