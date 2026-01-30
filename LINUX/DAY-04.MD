# Day-4

---

## Mastering the Linux Prompt

### Understanding the Linux Command Prompt

The **Linux Command Prompt** (also called the shell prompt or terminal prompt) is the place where you type commands to interact with the Linux system. It's like a conversation with your computer — you type a command, press Enter, and the computer executes it and shows you the result.

#### What is a Prompt?

A prompt is a text indicator that appears on your terminal screen, showing that the system is ready to accept your input. It's a signal saying: "I'm ready for your command!"

#### Example of a Command Prompt:

```bash
student@linux:~$
```

This simple line contains important information. Let's break it down!

---

## Decoding the Structure of the Command Prompt

The standard Linux command prompt has a specific structure. Understanding each part helps you navigate and interact with your system more effectively.

### Standard Prompt Format:

```bash
username@hostname:current_directory$
```

Let's analyze each component:

#### 1. **Username** (`student`)

```bash
student@linux:~$
└─────┘
```

**What it shows:**
- The username of the currently logged-in user
- In this case: `student`

**Different users, different prompts:**
```bash
# When logged in as 'student' user:
student@linux:~$

# When logged in as 'root' user:
root@linux:~#

# When logged in as 'john' user:
john@linux:~$
```

**Important Distinction:**
- Regular users: prompt ends with `$`
- Root user: prompt ends with `#`

---

#### 2. **@ Symbol** (`@`)

```bash
student@linux:~$
       ↑
```

**What it means:**
- Just a separator that means "at"
- Reads as: "student at linux"
- Divides username from hostname

---

#### 3. **Hostname** (`linux`)

```bash
student@linux:~$
         └────┘
```

**What it shows:**
- The name of your computer/server
- Helps identify which machine you're connected to (important when managing multiple servers)

**Examples:**
```bash
# Local computer named 'mycomputer'
student@mycomputer:~$

# Remote server named 'webserver01'
student@webserver01:~$

# Server in cloud
student@aws-prod-server:~$
```

**Why it matters:**
- When working with multiple servers, you always know which one you're on
- Prevents accidental commands on wrong server

---

#### 4. **Colon** (`:`)

```bash
student@linux:~$
              ↑
```

**What it means:**
- Another separator
- Divides hostname from current directory

---

#### 5. **Current Directory** (`~`)

```bash
student@linux:~$
              └─
```

**What it shows:**
- Your current location in the file system
- `~` is a shortcut meaning "home directory"
- Shows where your next command will be executed

**Examples of current directories:**
```bash
# In home directory
student@linux:~$

# In /home/student/Documents
student@linux:~/Documents$

# In /var/log
student@linux:/var/log$

# In root directory
student@linux:/$

# In /etc/nginx
student@linux:/etc/nginx$
```

---

#### 6. **Prompt Symbol** (`$` or `#`)

```bash
student@linux:~$
              ↑
```

**What it shows:**
- `$` = Regular user prompt (limited permissions)
- `#` = Root/superuser prompt (full permissions)

**Examples:**
```bash
# Regular user
student@linux:~$

# Root user
root@linux:~#

# Another regular user
teacher@linux:~$

# System user
www-data@linux:~$
```

---

### Complete Prompt Breakdown Example:

```bash
student@linux:~/Documents$
└─────┘ └────┘ └──────────┘┘
  |       |         |       └─ Prompt symbol ($ = regular user)
  |       |         └─ Current directory (~/Documents)
  |       └─ Hostname (computer name)
  └─ Username (who you are)
```

**What this means:**
- User `student` is logged in
- On computer named `linux`
- Currently in the `Documents` folder inside home directory
- Ready to accept commands

---

### Real-World Prompt Examples:

#### Example 1: Regular User at Home
```bash
john@ubuntu:~$
```
- User: john
- Computer: ubuntu
- Location: home directory
- Permissions: limited (regular user)

---

#### Example 2: Root User in System Directory
```bash
root@ubuntu:/etc/nginx#
```
- User: root
- Computer: ubuntu
- Location: /etc/nginx directory
- Permissions: full (root user)

---

#### Example 3: System User Running Service
```bash
www-data@webserver01:/var/www/html$
```
- User: www-data (web server user)
- Computer: webserver01
- Location: /var/www/html (web files)
- Permissions: limited (system user)

---

#### Example 4: Different User on Different Server
```bash
admin@prod-database:/home/admin$
```
- User: admin
- Computer: prod-database (production server)
- Location: /home/admin (home directory)
- Permissions: limited (but might have sudo access)

---

## Effective Command Prompt Usage: A Step-by-Step Guide

### Step 1: Understanding the Prompt

When you see the prompt, it means:
- The system is ready to accept commands
- Your previous command has finished executing
- You can type a new command

### Step 2: Basic Command Structure

Every command follows this pattern:

```bash
command [options] [arguments]
```

#### Components:

1. **Command** — What you want to do
   ```bash
   ls          ← command to list files
   mkdir       ← command to make directory
   ```

2. **Options** — How to modify the command (usually start with `-`)
   ```bash
   ls -l       ← -l is an option (long format)
   ls -a       ← -a is an option (show all files)
   ls -la      ← combine multiple options
   ```

3. **Arguments** — What to operate on
   ```bash
   ls /home    ← /home is the argument (list this directory)
   mkdir mydir ← mydir is the argument (create this directory)
   ```

---

### Step 3: Typing and Executing Commands

**The Process:**

```bash
1. See prompt: student@linux:~$
2. Type command: ls -l /home
3. Full line: student@linux:~$ ls -l /home
4. Press Enter to execute
5. System runs command and shows output
6. New prompt appears when done
```

**Visual Example:**

```bash
student@linux:~$ ls -l /home
total 24
drwxr-xr-x 5 student student 4096 Dec  5 10:00 student
drwxr-xr-x 3 teacher teacher 4096 Dec  4 09:30 teacher

student@linux:~$ 
↑
New prompt appears - ready for next command
```

---

### Step 4: Command Examples with Explanations

#### Example 1: List Files

```bash
student@linux:~$ ls
Desktop   Documents   Downloads   Music   Pictures   Videos
```

What happened:
- Typed `ls` (list files command)
- Command executed in current directory (~)
- Shows all files and folders in home directory

---

#### Example 2: List Files with Details

```bash
student@linux:~$ ls -l
total 40
drwxr-xr-x  3 student student 4096 Dec  5 10:15 Desktop
drwxr-xr-x  2 student student 4096 Dec  4 15:30 Documents
-rw-r--r--  1 student student  1024 Dec  3 11:20 notes.txt
```

What happened:
- Typed `ls -l` (list with details)
- `-l` option shows:
  - Permissions
  - Owner
  - File size
  - Date/time created

---

#### Example 3: Change Directory

```bash
student@linux:~$ cd Documents
student@linux:~/Documents$
```

What happened:
- Typed `cd Documents` (change directory)
- Moved into Documents folder
- Prompt changed to show new location (`~/Documents`)

---

#### Example 4: Create Directory

```bash
student@linux:~/Documents$ mkdir my_project
student@linux:~/Documents$ ls
my_project
```

What happened:
- Typed `mkdir my_project` (make directory)
- Created new folder called `my_project`
- `ls` shows the new folder exists

---

#### Example 5: Create File

```bash
student@linux:~/Documents$ touch hello.txt
student@linux:~/Documents$ ls -l
-rw-r--r-- 1 student student 0 Dec  5 10:30 hello.txt
```

What happened:
- Typed `touch hello.txt` (create file)
- Created empty file called `hello.txt`
- `ls -l` shows the file with its details

---

### Step 5: Understanding Command Output

After executing a command, you see:
1. **Command output** — Information the command returns
2. **New prompt** — Indicates command finished, ready for next one

```bash
student@linux:~$ pwd
/home/student
↑
Output: your current directory path

student@linux:~$
↑
New prompt appears - command completed
```

---

### Step 6: Error Handling

When you make a mistake, you get an error message:

```bash
student@linux:~$ cd nonexistent_folder
bash: cd: nonexistent_folder: No such file or directory
student@linux:~$
```

What happened:
- Tried to change to folder that doesn't exist
- System shows error message
- Prompt reappears
- You can try again

---

### Step 7: Command History

The system remembers your previous commands:

```bash
student@linux:~$ history
    1  ls
    2  cd Documents
    3  ls -l
    4  mkdir my_project
    5  touch hello.txt
student@linux:~$
```

**How to use history:**
```bash
# See last 10 commands
history 10

# Run a previous command using number
!2          ← runs command #2 (cd Documents)

# Run last command that starts with 'ls'
!ls

# Go through commands with arrow keys
↑ (up arrow)   ← previous command
↓ (down arrow) ← next command
```

---

### Step 8: Using Tab Completion

**Tab Completion** automatically completes your typing:

```bash
# Start typing:
student@linux:~$ cd Doc

# Press Tab, it auto-completes:
student@linux:~$ cd Documents$

# Saves time and prevents typos!
```

**How to use it:**
- Type first few letters of command or filename
- Press Tab key
- System completes it (if unambiguous)
- If multiple matches, press Tab twice to see all options

---

## Making the Command Prompt Your Own: Customization Tips (Advanced Concept)

### What Can You Customize?

You can change how your prompt looks and behaves by editing configuration files.

---

### Understanding the PS1 Variable

The prompt is controlled by a special variable called `PS1` (Prompt String 1).

#### View Current Prompt:

```bash
student@linux:~$ echo $PS1
\u@\h:\w$
```

This shows the prompt template.

---

### Prompt Variables Explained

| Variable | Shows | Example |
|----------|-------|---------|
| `\u` | Username | student |
| `\h` | Hostname | linux |
| `\w` | Current directory | ~/Documents |
| `\d` | Date | Wed Dec  5 |
| `\t` | Time (HH:MM:SS) | 10:30:45 |
| `\T` | Time (12-hour) | 10:30:45 AM |
| `\$` | $ or # symbol | $ (for user) or # (for root) |
| `\n` | New line | (starts on new line) |

---

### Example Customizations

#### Example 1: Simple Colored Prompt

```bash
# Edit the .bashrc file (configuration file)
nano ~/.bashrc

# Find the line with PS1= and change it to:
export PS1="\u@\h:\w\$ "

# Save and reload
source ~/.bashrc
```

#### Example 2: Colored Prompt with Time

```bash
# Add this to ~/.bashrc
export PS1="[\t] \u@\h:\w$ "
```

This shows:
```bash
[10:30:45] student@linux:~/Documents$
```

---

#### Example 3: Prompt with Colors

```bash
# Add to ~/.bashrc (advanced)
export PS1="\e[32m\u@\h\e[0m:\w$ "
```

This makes username green.

---

#### Example 4: Multi-line Prompt

```bash
# Add to ~/.bashrc
export PS1="\u@\h\n\w$ "
```

Shows as:
```bash
student@linux
~/Documents$
```

---

### How to Make Changes Permanent

1. **Open configuration file:**
   ```bash
   nano ~/.bashrc
   ```

2. **Find the PS1 line:**
   ```bash
   # Search for: PS1=
   ```

3. **Edit or add new PS1:**
   ```bash
   export PS1="your_custom_prompt_here"
   ```

4. **Save (Ctrl+O, Enter, Ctrl+X)**

5. **Reload configuration:**
   ```bash
   source ~/.bashrc
   ```

6. **See changes immediately:**
   ```bash
   # Your prompt should now look different!
   ```

---

### Useful Customizations for Students

#### Simple and Professional:
```bash
export PS1="\u@\h:\w$ "
```

#### With Git Branch (if in git directory):
```bash
export PS1="\u@\h:\w\$(git branch 2>/dev/null | grep '^\*' | colrm 1 2) $ "
```

#### With Current Date:
```bash
export PS1="\d \u@\h:\w$ "
```

#### Minimal and Clean:
```bash
export PS1="\w$ "
```

---

## Introduction to Linux Basic Commands

Now that you understand the prompt, let's learn essential Linux commands!

### Command Categories

1. **File and Directory Commands**
2. **Text Commands**
3. **System Information Commands**
4. **File Content Commands**
5. **Help Commands**

---

## Getting Started with the Linux Terminal

### What is the Terminal?

The terminal is the application window where you see the command prompt and type commands. It's your interface to the Linux command line.

### Opening Terminal

#### On Ubuntu/Debian:
- Right-click on desktop → "Open Terminal Here"
- Or press Ctrl+Alt+T
- Or search for "Terminal" in applications menu

#### On Other Systems:
- Find the Terminal or Console application
- Or SSH into a remote Linux server

---

### Terminal vs Prompt

| Term | Meaning |
|------|---------|
| **Terminal** | The application window |
| **Prompt** | The text line where you type |
| **Shell** | The program that interprets commands |
| **Command Line** | Where you type commands |

---

### First Steps in Terminal

When you open terminal:

```bash
student@linux:~$
```

1. You see your prompt
2. Cursor blinks (ready for input)
3. Type your command
4. Press Enter to execute

---

## Essential System Information: Commands and Tools for Linux

### Understanding System Information

System information tells you about your computer: CPU, RAM, disk space, OS version, etc.

---

### Command 1: `uname` — Unix Name

**Purpose:** Display system information

**Basic Usage:**
```bash
student@linux:~$ uname
Linux
```

**Shows:**
- The kernel name (Linux, Darwin for Mac, etc.)

---

**Detailed Information:**
```bash
student@linux:~$ uname -a
Linux ubuntu 5.15.0-84-generic #94-Ubuntu SMP Fri Oct 7 00:24:33 UTC 2022 x86_64 GNU/Linux
```

**Options:**
- `-a` — All information (kernel, hostname, kernel version, processor type)
- `-s` — Kernel name only
- `-r` — Kernel release
- `-v` — Kernel version
- `-m` — Machine hardware name (x86_64, ARM, etc.)

**What each part means:**
```
Linux              ← Kernel name
ubuntu             ← Hostname
5.15.0-84-generic  ← Kernel version
#94-Ubuntu         ← Build number
x86_64             ← Architecture (64-bit processor)
GNU/Linux          ← Operating system
```

---

### Command 2: `lsb_release` — Linux Standard Base Release

**Purpose:** Show Linux distribution information

**Basic Usage:**
```bash
student@linux:~$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Release:        20.04
Codename:       focal
```

**Options:**
- `-a` — All information
- `-d` — Distribution description
- `-r` — Release number
- `-c` — Codename

**What it shows:**
- Distributor: Which Linux distribution (Ubuntu, CentOS, etc.)
- Release: Version number (20.04, 22.04, etc.)
- Codename: Code name for that version (focal, jammy, etc.)

---

### Command 3: `whoami` — Who Am I

**Purpose:** Show the current logged-in user

**Usage:**
```bash
student@linux:~$ whoami
student
```

**Shows:**
- Your username

**When to use:**
- Verify which user account you're using
- Especially useful when logged into multiple systems

---

### Command 4: `id` — Identity

**Purpose:** Show user and group IDs

**Basic Usage:**
```bash
student@linux:~$ id
uid=1000(student) gid=1000(student) groups=1000(student),27(sudo),999(docker)
```

**What it shows:**
- `uid` — User ID number (1000)
- `gid` — Group ID number (1000)
- `groups` — All groups you belong to

**Detailed Breakdown:**
```
uid=1000(student)        ← User ID 1000, username is student
gid=1000(student)        ← Primary group ID 1000, group name is student
groups=1000(student)     ← Member of student group
       27(sudo)          ← Member of sudo group (can use sudo)
       999(docker)       ← Member of docker group
```

---

### Command 5: `hostname` — Computer Name

**Purpose:** Show or change the computer's name

**Usage:**
```bash
student@linux:~$ hostname
linux
```

**Shows:**
- Your computer's hostname

**Change hostname (requires sudo):**
```bash
sudo hostname newname
```

---

### Command 6: `pwd` — Print Working Directory

**Purpose:** Show your current directory

**Usage:**
```bash
student@linux:~$ pwd
/home/student
```

**Shows:**
- Your exact location in the file system

**Examples:**
```bash
# In home directory
student@linux:~$ pwd
/home/student

# In Documents folder
student@linux:~/Documents$ pwd
/home/student/Documents

# In system directory
student@linux:/etc$ pwd
/etc
```

---

### Command 7: `ls` — List Directory Contents

**Purpose:** Show files and folders

**Basic Usage:**
```bash
student@linux:~$ ls
Desktop   Documents   Downloads   Music   Pictures   Videos
```

**Common Options:**
```bash
# Long format with details
student@linux:~$ ls -l

# Show hidden files (starting with .)
student@linux:~$ ls -a

# Combined options
student@linux:~$ ls -la

# Show human-readable file sizes
student@linux:~$ ls -lh

# Sort by modification time
student@linux:~$ ls -lt

# Show only directories
student@linux:~$ ls -d */
```

**Output Explanation (ls -l):**
```bash
-rw-r--r-- 1 student student 1024 Dec 5 10:30 file.txt
│  │  │
│  │  └─ Others can read (r)
│  └──── Group can read (r)
└─────── Owner can read/write (rw)
```

---

### Command 8: `df` — Disk Free

**Purpose:** Show disk space usage

**Basic Usage:**
```bash
student@linux:~$ df
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/sda1      102081528 45032120 52309292  47% /
```

**Better Format:**
```bash
student@linux:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        98G   45G   50G  47% /
```

**What it shows:**
- `Filesystem` — Storage device name
- `Size` — Total disk space
- `Used` — Space used
- `Avail` — Space available
- `Use%` — Percentage used
- `Mounted on` — Where it's connected

---

### Command 9: `du` — Disk Usage

**Purpose:** Show how much space directories use

**Usage:**
```bash
student@linux:~$ du -sh ~/Documents
2.5G    /home/student/Documents
```

**Shows:**
- Total size of a directory

**Options:**
- `-s` — Summary (total only)
- `-h` — Human-readable (K, M, G)

**Examples:**
```bash
# Size of current directory
student@linux:~$ du -sh .
1.5G    .

# Size of all subdirectories
student@linux:~$ du -sh */
512M    Desktop
1.2G    Documents
256M    Downloads
```

---

### Command 10: `free` — Memory Information

**Purpose:** Show RAM usage

**Usage:**
```bash
student@linux:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:          7.7Gi       2.3Gi       1.2Gi      256Mi       4.2Gi       4.9Gi
Swap:         2.0Gi       0B          2.0Gi
```

**What it shows:**
- `total` — Total RAM installed (7.7 GB)
- `used` — RAM being used (2.3 GB)
- `free` — Available RAM (1.2 GB)
- `buff/cache` — Cache memory (4.2 GB)
- `available` — Usable memory (4.9 GB)

**Swap:**
- Extension of RAM using hard disk
- Used when RAM is full

---

### Command 11: `top` — System Monitor

**Purpose:** Show running processes and system stats

**Usage:**
```bash
student@linux:~$ top
```

**Shows:**
- Running processes
- CPU usage
- Memory usage
- Process IDs
- User running each process

**How to exit:**
- Press `q` to quit

**Key Information:**
- `PID` — Process ID
- `USER` — User running the process
- `%CPU` — CPU usage percentage
- `%MEM` — Memory usage percentage
- `COMMAND` — Program name

---

### Command 12: `ps` — Process Status

**Purpose:** Show running processes (snapshot)

**Basic Usage:**
```bash
student@linux:~$ ps
  PID TTY      STAT   TIME COMMAND
 1234 pts/0    Ss   0:00 bash
 1245 pts/0    R+   0:00 ps
```

**Better Usage:**
```bash
student@linux:~$ ps aux
```

**Shows all processes with details:**
```bash
USER       PID %CPU %MEM    VSZ   RSS TTY STAT START   TIME COMMAND
root         1  0.0  0.1  43896  6908 ?   Ss   10:00   0:05 /sbin/init
student   1234  0.0  0.2  21540  9876 pts/0 Ss 10:05   0:00 bash
student   1245  0.0  0.1  38900  6500 pts/0 R+ 10:30   0:00 ps aux
```

**Useful Options:**
```bash
# Find a specific process
ps aux | grep python

# Sort by CPU usage
ps aux --sort=-%cpu

# Show process tree
ps aux --forest
```

---

### Command 13: `uptime` — System Uptime

**Purpose:** Show how long system has been running

**Usage:**
```bash
student@linux:~$ uptime
 10:30:45 up 5 days, 3:45, 2 users, load average: 0.45, 0.52, 0.48
```

**What it shows:**
- `10:30:45` — Current time
- `up 5 days, 3:45` — System running for 5 days, 3 hours, 45 minutes
- `2 users` — Number of logged-in users
- `load average` — System load (CPU usage)

---

### Command 14: `date` — Current Date and Time

**Purpose:** Show current date and time

**Usage:**
```bash
student@linux:~$ date
Wed Dec  5 10:30:45 UTC 2024
```

**Custom Format:**
```bash
# Show date only
student@linux:~$ date +%Y-%m-%d
2024-12-05

# Show time only
student@linux:~$ date +%H:%M:%S
10:30:45

# Custom format
student@linux:~$ date "+%A, %B %d, %Y"
Wednesday, December 05, 2024
```

---

### Command 15: `which` — Locate Command

**Purpose:** Show where a command is located

**Usage:**
```bash
student@linux:~$ which python
/usr/bin/python

student@linux:~$ which ls
/bin/ls

student@linux:~$ which gcc
/usr/bin/gcc
```

**Shows:**
- The full path to the executable file

---

### Command 16: `man` — Manual Pages

**Purpose:** Get help for any command

**Usage:**
```bash
student@linux:~$ man ls
LS(1)                            User Commands                           LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List information about the FILEs...
```

**How to use:**
- `Space` — Page down
- `q` — Quit
- `/keyword` — Search
- `n` — Next match

**Examples:**
```bash
# Learn about ls command
man ls

# Learn about mkdir
man mkdir

# Learn about file permissions
man chmod
```

---

### Command 17: `type` — Command Type

**Purpose:** Show what type of command it is

**Usage:**
```bash
student@linux:~$ type ls
ls is aliased to `ls --color=auto'

student@linux:~$ type pwd
pwd is a shell builtin

student@linux:~$ type python
python is /usr/bin/python
```

**Shows:**
- If it's an alias
- If it's a built-in shell command
- If it's an external program (and where)

---

## Quick Reference: Essential Commands Summary

```bash
# System Information
uname -a              # Kernel and system info
lsb_release -a        # Linux distribution info
whoami                # Current user
id                    # User and group IDs
hostname              # Computer name
uptime                # System uptime
date                  # Current date and time

# Directory and Files
pwd                   # Print working directory
ls                    # List files
ls -l                 # List with details
ls -la                # List with hidden files
df -h                 # Disk space usage
du -sh                # Directory size

# Memory and Processes
free -h               # Memory usage
top                   # Real-time process monitor
ps aux                # Show all processes
ps aux | grep python  # Find specific process

# Help and Location
which command         # Find command location
man command           # Show command manual
type command          # Show command type
```

---

## Hands-On Exercises for Students

### Exercise 1: Explore Your System

```bash
# 1. Check your username
whoami

# 2. See your user ID and groups
id

# 3. Check your current location
pwd

# 4. See your Linux distribution
lsb_release -a

# 5. Check system uptime
uptime
```

---

### Exercise 2: Check Disk and Memory

```bash
# 1. See disk space
df -h

# 2. Check a specific directory size
du -sh ~/Documents

# 3. Check RAM usage
free -h

# 4. See which processes use most memory
top
```

---

### Exercise 3: Find and Learn About Commands

```bash
# 1. Find where ls command is
which ls

# 2. Get help about ls
man ls

# 3. Find python installation
which python

# 4. List all processes
ps aux | head
```

---

### Exercise 4: Customize Your Prompt

```bash
# 1. See current prompt setting
echo $PS1

# 2. Edit configuration
nano ~/.bashrc

# 3. Find PS1= line and change to:
export PS1="\u@\h:\w\$ "

# 4. Save and reload
source ~/.bashrc

# 5. See your new prompt!
```

---

## Common Command Usage Patterns

### Pattern 1: View Information About System

```bash
student@linux:~$ uname -a
student@linux:~$ lsb_release -a
student@linux:~$ whoami
```

### Pattern 2: Check Resource Usage

```bash
student@linux:~$ df -h
student@linux:~$ du -sh .
student@linux:~$ free -h
student@linux:~$ top
```

### Pattern 3: Monitor Processes

```bash
student@linux:~$ ps aux
student@linux:~$ ps aux | grep python
student@linux:~$ top
```

### Pattern 4: Get Help

```bash
student@linux:~$ man ls
student@linux:~$ which python
student@linux:~$ type python
```

---

## Key Takeaways for Students

1. **Prompt Structure:** `username@hostname:directory$`
   - Shows who you are, where you are, and what machine

2. **Command Execution:** Type command → Press Enter → See output → New prompt

3. **Navigation:** Use `pwd` to see location, `cd` to change location

4. **System Info:** Use commands like `uname`, `df`, `free`, `top` to check system

5. **Getting Help:** Use `man command` to learn about any command

6. **Tab Completion:** Use Tab to auto-complete commands and filenames

7. **Command History:** Use arrow keys or `history` to recall previous commands

8. **Customization:** Edit `~/.bashrc` to customize your prompt and environment


## Additional Basic Commands

| Command | Description |
|---------|-------------|
| `tty` | Displays current user terminal number. |
| `who` | Displays current logged-in users with their details. |
| `who am i` | Displays current user details. |
| `whoami` | Displays current user username. |
| `w` | Displays all current user details with their time schedule. |
| `wh <tab> <tab>` | To see similar commands or autocomplete cmd. |
| `clear` or `ctrl+l` | Clears screen but not background data. |
| `cal` | Displays current month of calendar. |
| `cal <year>` | Displays specified year calendar. |
| `cal <month> <year>` | Displays specific month's calendar in particular year. |
| `cal -3` | Displays previous, current, and next month's calendar of current year. |
| `cal -j <year>` | Displays Julian days of particular year. |
| `date` | Shows current date and time. |
| `date -s "DD MM YYYY HH:MM:SS"` | Sets date and time. |
| `reboot` or `init 6` | Restarts the system. |
| `poweroff` or `init 0` | Powers off the system. |
| `shutdown` | Shuts down system after 1 min. |
| `shutdown -h 10` | Shuts down system after 10 min and broadcasts message to all users. |
| `shutdown -c` | Cancels shutdown timer and broadcasts message to all users. |
| `shutdown now` or `shutdown -h` | Immediately shuts down system. |
| `logout` or `exit` or `ctrl + d` | Logs out from currently logged-in user. |
| `hostname` or `hostname -s` | Shows machine name. |

## Commands to View System Information

| Command | Description |
|---------|-------------|
| `hostnamectl` | Shows detailed information about system. |
| `uname -a` | Displays operating system kernel name. |
| `uname -r` | Displays all information regarding system. |
| `free -h` | Displays RAM information in human-readable form. |
| `lsusb` | Lists all available USB devices. |
| `lspci` | Lists all PCI devices. |
| `lscpu` | Lists processor information. |
| `dmidecode` | Displays all hardware information (requires root). |

## Commands for Getting Help

| Command | Description |
|---------|-------------|
| `man <command>` | Shows manual of mentioned command. |
| `info <command>` | Same as man command. |
| `whatis <command>` | Displays one-line description of manual page (use `mandb` to update database). |
| `<command> --help` | Shows short description of manual page (some commands may not support this). |
| `which <command>` | Shows path of command file. |

