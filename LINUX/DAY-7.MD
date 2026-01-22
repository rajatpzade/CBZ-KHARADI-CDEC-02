# Day-7


## Mastering Text Editing with VIM

### Overview of Vim and its History

**What is Vim?**
Vim (short for "Vi IMproved") is a powerful text editor that runs in the terminal. It's designed for fast and efficient text editing, especially for programmers and system administrators. Unlike simple editors like Notepad, Vim uses different "modes" to do different tasks, which might feel strange at first but becomes very powerful once you learn it.

**Why Use Vim?**
- **Speed:** Edit text quickly without a mouse.
- **Everywhere:** Available on almost every Linux system (and many others).
- **Powerful:** Supports advanced features like macros, plugins, and scripting.
- **Lightweight:** No fancy GUI needed, just runs in the terminal.

**History:**
- Vim is based on an older editor called Vi, created in 1976 by Bill Joy for Unix systems.
- Bram Moolenaar created Vim in 1991 as an improved version of Vi.
- Vim is free, open-source software and is the default editor on many Linux distributions.
- It's widely used in programming because it's efficient for handling code.

**Getting Started:**
- Install if needed: `sudo apt install vim` (on Ubuntu/Debian)
- Open a file: `vim filename.txt`
- Vim starts in "Normal mode" (also called Command mode).

---

### Basic Concepts: Modes in Vim

Vim works in different "modes," each for a specific purpose. This is the key to Vim's power. You switch between modes using keys.

#### 1. **Normal Mode (Command Mode)**
   - **Purpose:** Navigate, manipulate text, and run commands.
   - **Default Mode:** Vim opens here.
   - **Indicator:** No special message; cursor is a block.
   - **Common Actions:** Moving around, deleting text, copying/pasting.

#### 2. **Insert Mode**
   - **Purpose:** Type and edit text like a regular editor.
   - **How to Enter:** Press `i`, `a`, `o`, etc. (explained later).
   - **Indicator:** Cursor becomes thin; "-- INSERT --" appears at the bottom.
   - **Common Actions:** Typing text, basic editing.

#### 3. **Visual Mode**
   - **Purpose:** Select text for operations (like highlighting).
   - **How to Enter:** Press `v` (character), `V` (line), or `Ctrl+v` (block).
   - **Indicator:** Selected text is highlighted; "-- VISUAL --" at bottom.
   - **Common Actions:** Select and operate on blocks of text.

#### 4. **Command-Line Mode (Execute Mode)**
   - **Purpose:** Run advanced commands, save files, quit, etc.
   - **How to Enter:** Press `:` in Normal mode.
   - **Indicator:** `:` appears at bottom with cursor.
   - **Common Actions:** `:w` (save), `:q` (quit), `:wq` (save and quit).

**Key Tip:** Always go back to Normal mode (press `Esc`) before switching to another mode. This is how Vim stays efficient!

---

### Basic Navigation in Command Mode

In Normal mode, use keys to move the cursor. No mouse needed!

#### Basic Movement:
- `h` — Move left (one character)
- `j` — Move down (one line)
- `k` — Move up (one line)
- `l` — Move right (one character)

**Remember:** `h`, `j`, `k`, `l` are like arrow keys (left, down, up, right).

#### Word Navigation:
- `w` — Move to start of next word
- `b` — Move to start of previous word
- `e` — Move to end of current word

#### Line Navigation:
- `0` — Go to beginning of line
- `$` — Go to end of line
- `^` — Go to first non-blank character of line

#### Screen Navigation:
- `Ctrl+u` — Move up half a screen
- `Ctrl+d` — Move down half a screen
- `gg` — Go to top of file
- `G` — Go to bottom of file
- `:[number]` — Go to specific line (e.g., `:10` for line 10)

#### Search Navigation:
- `/pattern` — Search forward for "pattern"
- `?pattern` — Search backward for "pattern"
- `n` — Next match
- `N` — Previous match

**Example Session:**
1. Open file: `vim test.txt`
2. Move down 5 lines: `5j`
3. Go to line 20: `:20`
4. Search for "error": `/error`

---

### Text Manipulation

In Normal mode, manipulate text with single keystrokes.

#### Deleting Text:
- `x` — Delete character under cursor
- `dd` — Delete entire line
- `dw` — Delete word
- `d$` — Delete from cursor to end of line
- `d0` — Delete from cursor to beginning of line

#### Copying (Yanking) Text:
- `yy` — Copy entire line
- `yw` — Copy word
- `y$` — Copy from cursor to end of line

#### Pasting Text:
- `p` — Paste after cursor
- `P` — Paste before cursor

#### Changing Text:
- `cw` — Change word (delete word and enter Insert mode)
- `cc` — Change entire line
- `c$` — Change from cursor to end of line

**Examples:**
- Delete 3 lines: `3dd`
- Copy current line and paste below: `yyp`
- Change "old" to "new": Place cursor on "old", type `cw`, then "new"

---

### Undo and Redo

Mistakes happen! Vim has easy undo/redo.

- `u` — Undo last change
- `Ctrl+r` — Redo last undone change
- `U` — Undo all changes on current line

**Examples:**
- Type some text, then undo: `u`
- Undo again: `u`
- Redo: `Ctrl+r`

**Tip:** Vim's undo is powerful and can handle complex changes.

---

### Entering Insert Mode

To type text, switch to Insert mode from Normal mode.

- `i` — Insert before cursor
- `a` — Append after cursor
- `o` — Open new line below and insert
- `O` — Open new line above and insert
- `I` — Insert at beginning of line
- `A` — Append at end of line

**Examples:**
- Insert before word: Place cursor, press `i`, type text
- Add line below: `o`, type new line

---

### Editing Text in Insert Mode

Once in Insert mode, type like a regular editor.

- Type text normally
- Use `Backspace` or `Delete` to remove characters
- Use `Enter` for new lines

**Tip:** Keep sessions in Insert mode short; go back to Normal mode for navigation.

---

### Navigating and Editing in Insert Mode

While in Insert mode, you can still navigate and edit.

- **Navigation:** Use arrow keys (←, →, ↑, ↓) or `Ctrl` combinations
- **Editing:** `Ctrl+w` — Delete word backward
- `Ctrl+u` — Delete entire line

**Note:** Arrow keys work, but Vim experts prefer staying in Normal mode.

---

### Exiting Insert Mode

Always exit Insert mode to return to Normal mode.

- `Esc` — Exit Insert mode (back to Normal mode)

**Tip:** Press `Esc` often to avoid confusion.

---

## Hands-On Exercises for Students

1. **Basic Navigation:**
   - Open a file: `vim test.txt`
   - Move around using `h`, `j`, `k`, `l`
   - Go to line 5: `:5`

2. **Text Manipulation:**
   - Delete a line: `dd`
   - Copy and paste: `yy` then `p`
   - Change a word: `cw` then type new word

3. **Insert Mode Practice:**
   - Enter Insert mode: `i`, type "Hello Vim", press `Esc`
   - Add a line: `o`, type "New line", press `Esc`

4. **Undo/Redo:**
   - Delete a line: `dd`
   - Undo: `u`
   - Redo: `Ctrl+r`

5. **Save and Quit:**
   - Save: `:w`
   - Quit: `:q`
   - Save and quit: `:wq`

---

## Quick Reference Cheat-Sheet

### Modes:
- Normal: Default, navigate/manipulate
- Insert: Type text (`i`, `a`, `o`)
- Visual: Select text (`v`, `V`)
- Command: Execute commands (`:`)

### Navigation (Normal Mode):
- `h/j/k/l`: Left/Down/Up/Right
- `w/b/e`: Word forward/backward/end
- `0/$`: Line start/end
- `gg/G`: File top/bottom

### Manipulation:
- Delete: `x` (char), `dd` (line), `dw` (word)
- Copy: `yy` (line), `yw` (word)
- Paste: `p` (after), `P` (before)
- Change: `cw` (word), `cc` (line)

### Other:
- Undo: `u`
- Redo: `Ctrl+r`
- Enter Insert: `i`, `a`, `o`
- Exit Insert: `Esc`
- Save/Quit: `:w`, `:q`, `:wq`

---

## Key Takeaways for Students

- Vim uses modes: Learn to switch between Normal, Insert, Visual, and Command modes.
- Master Normal mode for efficiency — most editing happens here.
- Practice basic navigation and manipulation daily.
- Use `:help` in Vim for built-in help.
- Start with simple files; build up to complex editing.

Remember, Vim has a learning curve, but it's rewarding for productivity!