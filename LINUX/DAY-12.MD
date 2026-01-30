# Day-12

---

## Managing Users and Permissions in Linux (Links and sudo Deep Dive)

Welcome to Day 12! Today, we'll explore advanced concepts in Linux permissions: understanding link counts, hard vs soft links, and mastering sudo for privilege escalation. These tools are essential for efficient file management and secure system administration.

---

### Link Count Basics

**What are Links?**
Links in Linux are references to files or directories. They allow multiple names to point to the same data, saving space and enabling flexible file organization.

**Why Link Counts Matter:**
- **Track References:** Shows how many names point to the same file/directory
- **Space Management:** Understands when data can be safely deleted
- **System Integrity:** Helps maintain file system consistency

**Viewing Link Count:**
The link count appears in `ls -l` output as the number before owner name:
```bash
$ ls -l file.txt
-rw-r--r-- 2 user group 1024 Dec 15 10:30 file.txt
          ↑
       Link count (2)
```

---

### Link Count for Directories

Directory link counts are more complex than files because directories contain references to themselves and their contents.

#### How Directory Links Work:
- **Self Reference:** Every directory has a link to itself (`.`)
- **Parent Reference:** Every directory (except root) has a link to its parent (`..`)
- **Subdirectory Links:** Each subdirectory creates a link back to its parent

#### Examples:
```bash
# Root directory (/)
$ ls -ld /
drwxr-xr-x 19 root root 4096 Dec 15 10:30 /
            ↑
         Link count: 19
# Why 19? Root + 18 top-level directories

# Home directory
$ ls -ld /home
drwxr-xr-x 3 root root 4096 Dec 15 10:30 /home
           ↑
        Link count: 3
# Why 3? Self (.) + parent (..) + 1 user directory

# User's home directory
$ ls -ld /home/user
drwxr-xr-x 2 user user 4096 Dec 15 10:30 /home/user
           ↑
        Link count: 2
# Why 2? Self (.) + parent (..)
```

#### Key Points:
- Link count increases when subdirectories are created
- Removing subdirectories decreases the parent's link count
- The link count helps track directory structure integrity

---

### Link Count for Files

File link counts are simpler: they show how many names (hard links) point to the same data.

#### Regular Files:
- **Normal Count:** 1 (just the original file)
- **With Hard Links:** Increases by 1 for each hard link
- **Soft Links:** Don't affect the original file's count

#### Examples:
```bash
# Create a file
$ touch original.txt
$ ls -l original.txt
-rw-r--r-- 1 user user 0 Dec 15 10:30 original.txt
           ↑
        Link count: 1

# Create a hard link
$ ln original.txt hardlink.txt
$ ls -l original.txt hardlink.txt
-rw-r--r-- 2 user user 0 Dec 15 10:30 original.txt
-rw-r--r-- 2 user user 0 Dec 15 10:30 hardlink.txt
           ↑                           ↑
        Both show: 2               Both show: 2

# Create a soft link
$ ln -s original.txt softlink.txt
$ ls -l original.txt hardlink.txt softlink.txt
-rw-r--r-- 2 user user 0 Dec 15 10:30 original.txt
-rw-r--r-- 2 user user 0 Dec 15 10:30 hardlink.txt
lrwxrwxrwx 1 user user 12 Dec 15 10:30 softlink.txt -> original.txt
           ↑                           ↑                    ↑
        Still: 2                   Still: 2            Count: 1 (soft link itself)
```

#### Key Points:
- Hard links share the same link count
- Soft links have their own count of 1
- Data is only deleted when all hard links are removed

---

### Comparing Hard and Soft Links

Linux supports two types of links: hard links and soft (symbolic) links. They serve different purposes.

#### Hard Links:
- **What it is:** Direct pointer to the file's data on disk
- **Creation:** `ln source target`
- **Same Inode:** Shares the same inode number as original
- **Same Permissions:** Changes to one affect all (ownership, permissions)
- **Cross Filesystem:** Cannot span different filesystems
- **Directory Links:** Cannot create hard links to directories
- **Deletion:** File data persists until all hard links are deleted

#### Soft (Symbolic) Links:
- **What it is:** Pointer to the file's name/path, not data
- **Creation:** `ln -s source target`
- **Different Inode:** Has its own inode number
- **Independent Permissions:** Can have different permissions
- **Cross Filesystem:** Can span different filesystems
- **Directory Links:** Can link to directories
- **Deletion:** Broken if original is deleted (dangling link)

#### Comparison Table:

| Aspect | Hard Link | Soft Link |
|--------|-----------|-----------|
| **Command** | `ln file link` | `ln -s file link` |
| **Inode** | Same as original | Different |
| **Filesystem** | Same filesystem only | Can cross filesystems |
| **Directories** | Not allowed | Allowed |
| **Original Deletion** | Data persists | Link becomes broken |
| **Space Usage** | Minimal (just directory entry) | Minimal (just directory entry) |
| **ls -l Display** | Normal file appearance | Shows `-> target` |

#### When to Use Each:
- **Hard Links:** Backup important files, create multiple names for same data
- **Soft Links:** Link to directories, create shortcuts, span filesystems

---

### Importance of sudo for Privilege Escalation

**What is Privilege Escalation?**
Privilege escalation means temporarily gaining higher permissions (usually root) to perform administrative tasks.

**Why sudo is Important:**
- **Security:** Limits root access, logs all privileged actions
- **Accountability:** Tracks who ran what commands as root
- **Flexibility:** Grants specific permissions without full root access
- **Safety:** Prevents accidental system damage from regular users
- **Compliance:** Meets security standards requiring audit trails

**Risks Without sudo:**
- Users might share root passwords
- No audit trail of privileged actions
- Accidental system damage more likely
- Harder to restrict specific permissions

---

### Difference Between Regular User Commands and sudo Commands

Commands behave differently based on whether they're run as regular user or with sudo.

#### Regular User Commands:
- **Permissions:** Limited to user's files and allowed actions
- **Scope:** Can modify user's home directory, read some system files
- **Examples:**
  ```bash
  # Works: modify own files
  touch ~/myfile.txt
  
  # Fails: modify system files
  touch /etc/myfile.txt  # Permission denied
  ```

#### sudo Commands:
- **Permissions:** Full system access (as root)
- **Scope:** Can modify any file, run any command
- **Logging:** Actions are logged for audit
- **Examples:**
  ```bash
  # Works: modify system files
  sudo touch /etc/myfile.txt
  
  # Still works: user's files (but unnecessary)
  sudo touch ~/myfile.txt
  ```

#### Key Differences:

| Aspect | Regular User | sudo |
|--------|--------------|------|
| **Access Level** | Limited | Full (root) |
| **System Files** | Read-only (mostly) | Read/write |
| **Logging** | Not logged | Logged in /var/log/auth.log |
| **Password** | User's password | User's password (for sudo) |
| **Risk** | Low | High (if misused) |

---

### Configuring sudo Access

sudo access is controlled by the `/etc/sudoers` file. Never edit it directly—use `visudo`!

#### Basic sudoers Syntax:
```
username ALL=(ALL) ALL
%group ALL=(ALL) ALL
username ALL=(ALL) NOPASSWD: command
```

#### Common Configurations:
```bash
# Allow user full sudo access
rajat ALL=(ALL) ALL

# Allow group sudo access
%admin ALL=(ALL) ALL

# Allow specific command without password
rajat ALL=(ALL) NOPASSWD: /usr/bin/apt update

# Allow only specific commands
rajat ALL=(ALL) /usr/bin/apt, /usr/bin/systemctl
```

#### Using visudo:
```bash
# Edit sudoers file safely
sudo visudo

# Add line for user
rajat ALL=(ALL) ALL

# Save and exit (Ctrl+O, Enter, Ctrl+X)
```

#### Testing Configuration:
```bash
# Test sudo access
sudo whoami  # Should show 'root'

# Check sudo privileges
sudo -l
```

---

### sudo Command Syntax and Example

#### Basic Syntax:
```bash
sudo [options] command [arguments]
```

#### Common Options:
- `-u user` — Run as specific user (default: root)
- `-i` — Start interactive shell as root
- `-l` — List user's sudo privileges
- `-k` — Invalidate cached credentials

#### Examples:
```bash
# Run command as root
sudo apt update

# Run as specific user
sudo -u www-data whoami

# Start root shell
sudo -i

# List privileges
sudo -l

# Edit system file
sudo nano /etc/hosts

# Restart service
sudo systemctl restart apache2

# Install package
sudo apt install vim

# View root-only file
sudo cat /etc/shadow
```

#### Advanced Examples:
```bash
# Run multiple commands
sudo bash -c "apt update && apt upgrade"

# Preserve environment
sudo -E env

# Run with specific working directory
sudo -u apache -H bash -c "cd /var/www && ls"
```

---

## Hands-On Exercises for Students

1. **Explore Link Counts:**
   ```bash
   # Check file link counts
   touch file1.txt
   ln file1.txt file2.txt
   ls -l file1.txt file2.txt
   
   # Check directory link counts
   mkdir testdir
   cd testdir
   mkdir subdir
   ls -ld /home/user/testdir
   cd ..
   ```

2. **Create and Compare Links:**
   ```bash
   # Create hard link
   ln original.txt hardlink.txt
   ls -li original.txt hardlink.txt  # Same inode
   
   # Create soft link
   ln -s original.txt softlink.txt
   ls -li original.txt softlink.txt  # Different inodes
   
   # Test deletion behavior
   rm original.txt
   ls -l hardlink.txt softlink.txt
   ```

3. **Practice sudo:**
   ```bash
   # Test basic sudo
   sudo whoami
   
   # Edit system file
   sudo nano /etc/hostname
   
   # Check privileges
   sudo -l
   
   # Run as different user
   sudo -u daemon whoami
   ```

4. **Configure sudo (Carefully!):**
   ```bash
   # View current sudoers (don't edit directly)
   sudo cat /etc/sudoers
   
   # Add user to sudo group (safer approach)
   sudo usermod -aG sudo username
   
   # Test new access
   su - username
   sudo whoami
   ```

5. **Link Scenarios:**
   ```bash
   # Create directory structure and check links
   mkdir -p parent/child/grandchild
   ls -ld parent parent/child parent/child/grandchild
   
   # Create links and observe counts
   ln -s /etc/passwd mypasswd
   ln /etc/hosts myhosts
   ls -l mypasswd myhosts
   ```

---