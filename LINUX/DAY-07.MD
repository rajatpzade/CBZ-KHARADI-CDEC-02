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


#  Editors in Linux

Editors are used to create new files, and edit or modify the content inside it. Simply editors 
are used to read and write data in existing or newly created file. Editors can be classified on the basis 
of interfaces that they use, i.e. Graphical Editors and Command Line Editors.

### Graphical Editors

Graphical editors use graphical user interfaces. They are easy to use but consume more memory 
than command line editors. In Linux, following are some well-known graphical editors:

1. **gedit**: It is similar to Notepad in Windows. You can open gedit graphically in the application 
menu and also using the command `$ gedit`.
2. **kedit**: It is similar to gedit but contains some advanced features. Generally, you have to install 
kedit separately to use it.
3. **Open Office**: Open Office is similar to MS Office. This Open Office is specially developed 
for Linux-based operating systems.

### Command Line Editors

Command line editors use command line interfaces. These editors are much more efficient and 
consume less memory than graphical editors. Following are some well-known command line 
editors:

1. **nano**: The nano editor is easy to use since it provides simple features to edit data from files.
   - Syntax: `# nano <filename>.<extension>`
2. **pico**: 
   - Syntax: `# pico <filename>`
3. **vi and vim**: vi (virtual interface) and vim (virtual interface modified) are most commonly used 
editors. vi and vim are the same, whereas vim is the advanced version of the vi editor. 
Thus, it contains some additional features. These editors work in four different modes:
   - Insert mode
   - Ex-mode 
   - Command mode
   - Visual mode
   
   Syntax: `# vim <filename>`
   
   **Command Mode**: This is the default mode. Press `Esc` to exit from any mode and 
   enter into command mode.
   
   | Command | Description |
   |---------|-------------|
   | `dd` | Delete current line |
   | `<n>dd` | Delete n no. of lines from current line |
   | `dw` | Delete current word |
   | `<n>dw` | Delete n no. of words from current word |
   | `yy` | Copy current line |
   | `<n>yy` | Copy n no. of lines from current line |
   | `yw` | Copy current word |
   | `<n>yw` | Copy n no. of words from current word |
   | `cc` | Cut current line and enter in insert mode |
   | `<n>cc` | Cut n no. of lines and enter in insert mode |
   | `cw` | Cut current word and enter in insert mode |
   | `<n>cw` | Cut n no. of words from current word and enter in insert mode |
   | `p` | Paste |
   | `s` | Remove current character and enter in insert mode |
   | `S` | Remove current line and enter in insert mode |
   | `u` | Undo |
   | `Ctrl+r` | Redo |
   | `H` | Move cursor to the top of screen |
   | `M` | Move cursor to the middle of screen |
   | `L` | Move cursor to the bottom of screen |
   | `G` | Move cursor at the end of file |
   | `gg` | Move cursor at the beginning |
   | `<n>gg` | Move cursor at nth line |
   | `/<word>` | Search particular word/string/character |
   | `n` | Show next search result |
   | `N` | Show previous search result |

## Mastering Text Editing with VIM

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
   
   **Commands to Enter Insert Mode:**
   - `i` — Insert text at current cursor position
   - `I` — Insert text at start of the current line
   - `a` — Insert text just right of the current character
   - `A` — Insert text at end of the current line
   - `o` — Insert new line below the current line
   - `O` — Insert new line above the current line
   - `r` — Replace single character
   - `R` — Replace multiple characters

#### 3. **Visual Mode**
   - **Purpose:** Select text for operations (like highlighting).
   - **How to Enter:** Press `v` (character), `V` (line), or `Ctrl+v` (block).
   - **Indicator:** Selected text is highlighted; "-- VISUAL --" at bottom.
   - **Common Actions:** Select and operate on blocks of text.
   
   **Visual Mode Selection:**
   - `v` — Select character by character
   - `V` — Select line by line
   - `Ctrl+v` — Select block
   - After selection: `y` (copy), `d` (delete), `c` (cut) for the selected area

#### 4. **Command-Line Mode (Execute Mode or Ex-mode)**
   - **Purpose:** Run advanced commands, save files, quit, etc.
   - **How to Enter:** Press `:` in Normal mode.
   - **Indicator:** `:` appears at bottom with cursor.
   - **Common Actions:** `:w` (save), `:q` (quit), `:wq` (save and quit).
   
   **Ex-mode Commands:**
   - `:q` — Quit without saving
   - `:q!` — Quit without saving forcefully
   - `:w` — Save and stay in file
   - `:wq` or `:x` — Save and quit
   - `:wq!` — Save and quit forcefully
   - `:set nu` — Set line numbers
   - `:<n>` — Jump to nth line
   - `:set nonu` — Remove line numbers
   - `:/<word>` — Highlight word/string/character
   - `:nohl` — Remove highlight
   - `:%s/<old>/<new>/g` — Find and replace old word with new word globally
   - `:!<command>` — Execute any command on terminal without leaving editor

**Key Tip:** Always go back to Normal mode (press `Esc`) before switching to another mode. This is how Vim stays efficient!
