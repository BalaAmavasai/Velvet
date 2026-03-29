# Velvet (Vim Element Layout View Editor Tool)
Created by Bala Amavasai &lt;<bala.amavasai@gmail.com>&gt; & Claude Code

A modal, Vim-inspired code editor that runs entirely in your browser — no build step, no server, no dependencies.

![license](https://img.shields.io/badge/license-MIT-89b4fa?style=flat-square)
![zero dependencies](https://img.shields.io/badge/dependencies-none-a6e3a1?style=flat-square)
![single file](https://img.shields.io/badge/size-single%20file-cba6f7?style=flat-square)

---

## Overview

Velvet is a fully self-contained Vim emulator built in plain HTML and JavaScript. Drop the file into any web server or open it directly in a browser and start editing. It supports the core Vim editing model — modal input, operators, motions, text objects, macros, registers, marks — along with practical browser features like real file save/open, syntax highlighting, and multiple buffers.

## Demo

Open `vim-editor.html` directly in your browser. No install required.

```bash
git clone https://github.com/BalaAmavasai/velvet.git
open velvet/vim-editor.html
```

---

## Files

| File | Description |
|---|---|
| `vim-editor.html` | The editor — this is the entire application |
| `velvet-docs.html` | Full interactive reference documentation |

---

## Features

### Editor
- **Zero dependencies** — a single `.html` file, works offline
- **Syntax highlighting** — keywords, strings, numbers, comments, and functions (JavaScript-focused)
- **Multiple buffers** — tab bar with `:tabnew`, `:bn`, `:bp`, `Ctrl+→/←`
- **File I/O** — native Save/Open dialogs via the File System Access API (Chrome/Edge); download + `<input>` fallback for Firefox/Safari
- **Auto-pair** — `(`, `[`, `{`, `"`, `'`, `` ` `` with smart skip-over of closing chars
- **Auto-indent** — new lines inherit indentation; extra indent level after `{` or `:`
- **Line numbers** — absolute or relative

### Vim Compatibility
- **Modes** — Normal, Insert, Visual (char and line), Replace, Command, Search
- **Motions** — `hjkl`, `w/W/b/B/e`, `f/F/t/T`, `0/^/$`, `gg/G`, `%`, `{/}`, `H/M/L`
- **Operators** — `d`, `c`, `y`, `>`, `<` — all compose with motions and text objects
- **Text objects** — `iw/aw`, `i(/a(`, `i[/a[`, `i{/a{`, `i"/a"`, `i'/a'`, `` i`/a` ``
- **Search** — `/` and `?` with JavaScript regex, `n/N`, `*/#` (word under cursor)
- **Substitution** — `:%s/pattern/replacement/g` and `:s/…/…/g`
- **Undo/Redo** — 200-level stack per buffer (`u` / `Ctrl+r`)
- **Macros** — record with `q{reg}`, replay with `@{reg}`
- **Named registers** — `"a` through `"z`
- **Marks** — `m{a-z}` to set, `'{a-z}` to jump
- **Count prefixes** — e.g. `5j`, `3dd`, `2w` work as expected

---

## Quick Start

| Want to… | Do this |
|---|---|
| Start typing | Press `i` |
| Return to Normal mode | Press `Esc` |
| Save the file | `:w` or `Ctrl+S` |
| Open a file | `:e` or `Ctrl+O` |
| Search | `/pattern` then `n` / `N` |
| Run a command | `:` |

---

## Key Reference

### Modes

| Key | Mode |
|---|---|
| `i` / `a` / `o` | Insert |
| `v` / `V` | Visual / Visual Line |
| `R` | Replace |
| `:` | Command |
| `Esc` | → Normal |

### Navigation

| Key | Action |
|---|---|
| `h j k l` | ← ↓ ↑ → |
| `w` / `b` / `e` | Word forward / back / end |
| `0` / `^` / `$` | Line start / first non-blank / end |
| `gg` / `G` | File start / end |
| `{N}G` | Go to line N |
| `%` | Jump to matching bracket |
| `f{c}` / `t{c}` | Find / till char on line |
| `;` / `,` | Repeat f/t forward / backward |
| `{` / `}` | Paragraph backward / forward |
| `Ctrl+d` / `Ctrl+u` | Half-page down / up |
| `Ctrl+f` / `Ctrl+b` | Page down / up |

### Editing

| Key | Action |
|---|---|
| `dd` | Delete line |
| `yy` / `Y` | Yank (copy) line |
| `p` / `P` | Paste after / before |
| `u` / `Ctrl+r` | Undo / redo |
| `>>` / `<<` | Indent / de-indent |
| `~` | Toggle case of character |
| `r{c}` | Replace character under cursor |
| `J` | Join line with line below |
| `ciw` / `diw` | Change / delete inner word |
| `ci(` / `di{` | Change / delete inside brackets |
| `x` / `X` | Delete char under / before cursor |

### File & Buffer Commands

| Command | Action |
|---|---|
| `:w` | Save (native dialog on first save) |
| `:w {name}` | Save as |
| `:wa` | Save all buffers |
| `:e` | Open file picker |
| `:q` / `:q!` | Close / force close |
| `:wq` / `:x` | Save and close |
| `:tabnew` | New empty buffer |
| `:bn` / `:bp` | Next / previous buffer |
| `Ctrl+S` | Quick save |
| `Ctrl+O` | Quick open |

### Search & Replace

```
/pattern           search forward (supports regex)
?pattern           search backward
n / N              next / previous match
*                  search word under cursor (forward)
#                  search word under cursor (backward)
:noh               clear highlights

:s/old/new/g       replace on current line
:%s/old/new/g      replace in entire file
:%s/old/new/gi     case-insensitive
```

### Macros & Registers

```
qa        start recording into register 'a'
q         stop recording
@a        replay macro 'a'
10@a      replay 10 times

"ayy      yank line into register 'a'
"ap       paste from register 'a'
```

### Settings

| Command | Effect |
|---|---|
| `:set number` | Show line numbers |
| `:set relativenumber` | Relative line numbers |
| `:set nonumber` | Hide line numbers |
| `:set syntax=on/off` | Toggle syntax highlighting |
| `:set expandtab` | Use spaces for Tab |
| `:set tabstop=4` | Set tab width |

---

## Browser Compatibility

| Browser | Save | Open |
|---|---|---|
| Chrome 86+ | Native Save dialog; subsequent `:w` writes in place | Native Open dialog |
| Edge 86+ | Same as Chrome | Same as Chrome |
| Firefox | File download | `<input type="file">` picker |
| Safari | File download | `<input type="file">` picker |

---

## Extending Velvet

Everything lives in a single HTML file. Key areas to modify:

- **`highlightLine()`** — add support for more languages
- **`executeCommand()`** — add new `:` commands
- **`handleNormalKey()`** — add Normal mode bindings
- **`createBuffer()`** — extend the buffer data model

---

## License

MIT — free to use, modify, and distribute.
