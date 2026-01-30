# Day-9

---

## Managing Users and Permissions in Linux

 Today, we'll explore user and permission management in Linux. This is crucial for system administration, security, and multi-user environments. We'll cover creating users, managing groups, permissions, and switching between users safely.

---

### Overview of User and Permission Management

**What is User Management?**
User management involves creating, modifying, and removing user accounts on a Linux system. Each user has their own space, permissions, and identity.

**Why Important?**
- **Security:** Isolates users and prevents unauthorized access
- **Multi-user Support:** Allows multiple people to use the system safely
- **Resource Control:** Limits what each user can do
- **Auditing:** Tracks who did what

**Key Concepts:**
- **Users:** Individuals with accounts on the system
- **Groups:** Collections of users with shared permissions
- **Permissions:** What users can do with files and processes
- **Root:** Superuser with full system access

**Permission Types:**
- **Read (r):** View file contents
- **Write (w):** Modify file contents
- **Execute (x):** Run file as program

---

### Types of Users

Linux has different user types, each with specific roles and permissions.

#### 1. **Root User (Superuser)**
- **UID:** 0
- **Purpose:** Full system access, can do anything
- **Prompt:** Ends with `#`
- **Risk:** High — mistakes can break the system
- **Usage:** System administration tasks

#### 2. **Regular Users**
- **UID:** 1000+ (typically)
- **Purpose:** Normal users with limited permissions
- **Prompt:** Ends with `$`
- **Safety:** Protected from system damage
- **Example:** student, john, admin

#### 3. **System Users**
- **UID:** 1-999
- **Purpose:** Run system services and daemons
- **Login:** Usually disabled (no password)
- **Examples:** www-data (web server), mysql (database)

#### 4. **Service Users**
- **Purpose:** Dedicated accounts for specific services
- **Examples:** apache, nginx, postgres

**Check Current User:**
```bash
whoami          # Shows your username
id              # Shows UID, GID, and groups
```

---

### Using useradd Command

The `useradd` command creates new user accounts.

#### Basic Syntax:
```bash
useradd [options] username
```

#### Common Options:
- `-m` — Create home directory
- `-s /bin/bash` — Set default shell
- `-g group` — Set primary group
- `-G groups` — Set secondary groups
- `-c "Comment"` — Add comment/description
- `-d /path` — Set custom home directory

#### Examples:
```bash
# Create basic user with home directory
sudo useradd -m john

# Create user with specific shell and comment
sudo useradd -m -s /bin/bash -c "John Doe" john

# Create user with custom home and groups
sudo useradd -m -d /home/john -g users -G sudo john
```

**After useradd:**
- User is created but has no password (can't login yet)
- Home directory is created if `-m` used
- Default files are copied from `/etc/skel`

---

### Setting User Passwords

New users need passwords to login. Use `passwd` command.

#### Basic Usage:
```bash
sudo passwd username
```

#### Examples:
```bash
# Set password for new user
sudo passwd john
# Enter password when prompted

# Change your own password
passwd
# Enter current password, then new password

# Force password change on next login
sudo passwd -e john
```

**Password Requirements:**
- Minimum length (usually 8+ characters)
- Complexity rules (uppercase, lowercase, numbers)
- Configured in `/etc/security/pwquality.conf`

---

### Managing User Groups

Groups organize users for shared permissions.

#### Key Commands:

**Create Group:**
```bash
sudo groupadd groupname
# Example: sudo groupadd developers
```

**Add User to Group:**
```bash
sudo usermod -aG groupname username
# Example: sudo usermod -aG developers john
```

**Remove User from Group:**
```bash
sudo gpasswd -d username groupname
# Example: sudo gpasswd -d john developers
```

**Delete Group:**
```bash
sudo groupdel groupname
# Example: sudo groupdel developers
```

**View Groups:**
```bash
groups username     # Show user's groups
id username         # Show UID/GID and groups
cat /etc/group      # View all groups
```

#### Primary vs Secondary Groups:
- **Primary Group:** Default group for new files (usually username)
- **Secondary Groups:** Additional groups for permissions

---

### Removing Users

Remove users when they're no longer needed.

#### Basic Command:
```bash
sudo userdel username
```

#### Options:
- `-r` — Remove home directory and mail spool
- `-f` — Force removal even if user is logged in

#### Examples:
```bash
# Remove user but keep home directory
sudo userdel john

# Remove user and home directory
sudo userdel -r john

# Force remove (dangerous)
sudo userdel -rf john
```

**Caution:** Always backup data before removing users!

---

### Introduction to Affected Files

User management modifies several system files.

#### Key Files:

**`/etc/passwd`**
- Stores user account information
- Format: username:password:x:uid:gid:comment:home:shell
- Readable by all users

**`/etc/shadow`**
- Stores encrypted passwords
- Readable only by root
- Format: username:encrypted_password:...

**`/etc/group`**
- Stores group information
- Format: groupname:password:x:gid:userlist

**`/etc/gshadow`**
- Stores group passwords (rarely used)
- Readable only by root

**`/etc/skel`**
- Skeleton directory for new user homes
- Files copied to new user directories

---

### User Home Directories

Each user gets their own home directory for personal files.

#### Default Location:
- `/home/username` for regular users
- `/root` for root user

#### What's Created:
- When using `useradd -m`, creates `/home/username`
- Copies files from `/etc/skel` (like `.bashrc`, `.profile`)

#### Permissions:
- Owned by user (drwxr-xr-x username username)
- Private space for user's files

#### Managing Home Directories:
```bash
# List home contents
ls -la /home/username

# Change ownership
sudo chown -R username:group /home/username

# Backup home directory
sudo cp -r /home/username /backup/username-$(date +%F)
```

---

### Configuration Files

Several config files control user behavior.

#### `/etc/login.defs`
- Default settings for user creation
- UID/GID ranges, password policies

#### `/etc/default/useradd`
- Default options for useradd
- Default shell, home directory prefix

#### `~/.bashrc` and `~/.profile`
- User-specific shell configuration
- Aliases, environment variables, PATH

#### `/etc/bash.bashrc`
- System-wide bash configuration

#### Example: Customize User Shell
```bash
# Edit user's .bashrc
sudo nano /home/username/.bashrc

# Add alias
echo "alias ll='ls -lah'" >> /home/username/.bashrc
```

---

### Switching Between Users in Linux

Switch users without logging out.

#### Why Switch?
- Test permissions
- Run commands as different user
- Access restricted resources

#### Methods:
1. **su Command:** Switch user (requires password)
2. **sudo Command:** Run commands as other user (usually root)

---

### Using su Command

`su` (substitute user) switches to another user account.

#### Basic Usage:
```bash
su username
```

#### Examples:
```bash
# Switch to root
su

# Switch to specific user
su john

# Switch and run command
su -c "whoami" john

# Switch with login shell
su - john
```

**Notes:**
- Requires target user's password
- `su -` loads user's full environment
- `su` without `-` keeps current environment

---

### Using Sudo Command

`sudo` (superuser do) runs commands as another user, usually root.

#### Basic Usage:
```bash
sudo command
```

#### Examples:
```bash
# Run command as root
sudo apt update

# Run as specific user
sudo -u john whoami

# Edit file as root
sudo nano /etc/hosts

# List sudo privileges
sudo -l
```

#### Configuration:
- Configured in `/etc/sudoers`
- Use `visudo` to edit safely
- Format: `username ALL=(ALL) ALL`

#### Sudo vs Su:
- **sudo:** Temporary elevation, logs actions
- **su:** Full session switch, requires password each time

---

## Hands-On Exercises for Students

1. **Create a New User:**
   ```bash
   sudo useradd -m testuser
   sudo passwd testuser
   su testuser
   whoami
   exit
   ```

2. **Manage Groups:**
   ```bash
   sudo groupadd testgroup
   sudo usermod -aG testgroup testuser
   groups testuser
   ```

3. **Switch Users:**
   ```bash
   sudo -u testuser whoami
   su - testuser
   pwd
   exit
   ```

4. **Explore User Files:**
   ```bash
   cat /etc/passwd | grep testuser
   ls -la /home/testuser
   ```

5. **Clean Up:**
   ```bash
   sudo userdel -r testuser
   sudo groupdel testgroup
   ```

---

## Quick Reference Cheat-Sheet

### User Management:
- `useradd -m username` — Create user
- `passwd username` — Set password
- `usermod -aG group username` — Add to group
- `userdel -r username` — Remove user

### Groups:
- `groupadd group` — Create group
- `groupdel group` — Delete group
- `groups username` — Show user's groups

### Switching Users:
- `su username` — Switch user
- `sudo command` — Run as root
- `sudo -u user command` — Run as specific user

### Files:
- `/etc/passwd` — User info
- `/etc/group` — Group info
- `/home/username` — User home

---

## Key Takeaways for Students

- User management ensures security and organization.
- Root has unlimited power; use sudo for safety.
- Groups share permissions efficiently.
- Always backup before removing users.
- Practice on test users, not production systems!

Remember, with great power comes great responsibility. Use these tools wisely!