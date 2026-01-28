# Day-10


## Managing Users and Permissions in Linux (Advanced)

Welcome to Day 10! Building on Day 9, we'll dive deeper into password security, account management, and advanced group operations. These concepts are essential for maintaining a secure and well-organized Linux system.

---

### Importance of Password Security

**Why Password Security Matters:**
- **Protects User Accounts:** Prevents unauthorized access to personal data and system resources
- **System Integrity:** Stops attackers from compromising the entire system
- **Compliance:** Meets security standards and regulations
- **Data Protection:** Safeguards sensitive information

**Key Principles:**
- **Complexity:** Use mix of uppercase, lowercase, numbers, symbols
- **Length:** Minimum 8-12 characters (longer is better)
- **Uniqueness:** Different passwords for different accounts
- **Regular Changes:** Update passwords periodically
- **No Sharing:** Never share passwords

**Common Threats:**
- Brute force attacks (trying many passwords)
- Dictionary attacks (common words)
- Social engineering (tricking users)
- Keyloggers and phishing

---

### Using passwd Command

The `passwd` command manages user passwords. It's used by both users and administrators.

#### Basic Usage:
```bash
passwd [options] [username]
```

#### For Regular Users (Change Own Password):
```bash
passwd
# Prompts for current password, then new password twice
```

#### For Administrators (Change Other Users' Passwords):
```bash
sudo passwd username
# Only prompts for new password (no current password needed)
```

#### Common Options:
- `-l` — Lock user account
- `-u` — Unlock user account
- `-e` — Expire password (force change on next login)
- `-d` — Delete password (set to empty)
- `-S` — Show password status

#### Examples:
```bash
# Change your password
passwd

# Change another user's password
sudo passwd john

# Lock a user account
sudo passwd -l john

# Unlock a user account
sudo passwd -u john

# Force password change
sudo passwd -e john

# Check password status
sudo passwd -S john
```

---

### Password Policy Settings

Linux enforces password policies to ensure strong passwords.

#### Configuration Files:
- **`/etc/security/pwquality.conf`** — Password quality rules
- **`/etc/login.defs`** — General login settings

#### Key pwquality.conf Settings:
```
minlen = 8          # Minimum length
minclass = 3        # Minimum character classes (upper, lower, digit, special)
maxrepeat = 3       # Maximum consecutive same characters
maxsequence = 3     # Maximum monotonic character sequences
dictcheck = 1       # Check against dictionary words
usercheck = 1       # Check if password contains username
```

#### login.defs Settings:
```
PASS_MAX_DAYS=90     # Maximum password age
PASS_MIN_DAYS=1      # Minimum days between changes
PASS_WARN_AGE=7      # Warning days before expiration
```

#### Testing Password Policy:
```bash
# Test a password against policy
echo "testpassword" | pwscore
# Shows score and suggestions
```

---

### Account Locking and Expiration

Control user account access through locking and expiration.

#### Account Locking:
- **Purpose:** Temporarily disable login without deleting account
- **Methods:** passwd command or usermod

```bash
# Lock with passwd
sudo passwd -l username

# Lock with usermod
sudo usermod -L username

# Unlock
sudo passwd -u username
sudo usermod -U username
```

#### Account Expiration:
- **Purpose:** Automatically disable account after certain date
- **Use chage command** (explained below)

---

### Understanding /etc/shadow fields

The `/etc/shadow` file stores encrypted passwords and account information. Only root can read it.

#### File Format:
Each line represents one user:
```
username:password:lastchange:minage:maxage:warn:inactive:expire:reserved
```

#### Field Meanings:
1. **username** — User login name
2. **password** — Encrypted password (or ! for locked, * for no password)
3. **lastchange** — Days since Jan 1, 1970 password was last changed
4. **minage** — Minimum days between password changes
5. **maxage** — Maximum days password is valid
6. **warn** — Days before expiration to warn user
7. **inactive** — Days after expiration until account is disabled
8. **expire** — Date when account expires (days since Jan 1, 1970)
9. **reserved** — Reserved for future use

#### Example Entry:
```
john:$6$abc123$encryptedpassword:18500:0:90:7:30:19000:
```

**Reading the entry:**
- User: john
- Password: encrypted
- Last changed: 18500 days ago (~50 years)
- Min age: 0 days
- Max age: 90 days
- Warn: 7 days before expiration
- Inactive: 30 days after expiration
- Expires: 19000 days from epoch

---

### Using chage Command

`chage` (change age) manages password aging and account expiration.

#### Basic Usage:
```bash
sudo chage [options] username
```

#### Interactive Mode:
```bash
sudo chage john
# Prompts for all settings interactively
```

#### Command-Line Options:
- `-m days` — Set minimum password age
- `-M days` — Set maximum password age
- `-W days` — Set warning days
- `-I days` — Set inactive days
- `-E date` — Set account expiration date
- `-l` — List current settings

#### Examples:
```bash
# Set maximum age to 60 days
sudo chage -M 60 john

# Set expiration to specific date (YYYY-MM-DD)
sudo chage -E 2024-12-31 john

# List current settings
sudo chage -l john

# Set warning to 14 days
sudo chage -W 14 john
```

#### Date Formats:
- **Days since epoch:** `chage -E 19000`
- **YYYY-MM-DD:** `chage -E 2024-12-31`
- **Days from today:** `chage -E $(date -d '+30 days' +%Y-%m-%d)`

---

### Introduction to Linux Groups

Groups organize users for shared permissions and resource access.

**Why Groups Matter:**
- **Shared Access:** Multiple users can access same files
- **Permission Management:** Easier to manage permissions for groups than individuals
- **Resource Control:** Limit access to specific resources
- **Collaboration:** Teams can share files securely

**Group Concepts:**
- **Primary Group:** Default group for new files (usually matches username)
- **Secondary Groups:** Additional groups for extra permissions
- **GID:** Group ID number (like UID for users)

---

### Fields of /etc/group and /etc/gshadow

#### /etc/group File:
Stores group information, readable by all users.

**Format:**
```
groupname:password:GID:userlist
```

**Fields:**
1. **groupname** — Group name
2. **password** — Group password (usually x, actual password in gshadow)
3. **GID** — Group ID number
4. **userlist** — Comma-separated list of users in group

**Example:**
```
developers:x:1001:john,mary,bob
```

#### /etc/gshadow File:
Stores group passwords and administrators. Only root can read.

**Format:**
```
groupname:password:administrators:members
```

**Fields:**
1. **groupname** — Group name
2. **password** — Encrypted group password
3. **administrators** — Users who can change group password
4. **members** — Group members

**Example:**
```
developers:!::john,mary,bob
```

---

### Types of Groups

#### 1. **User Private Groups**
- **Purpose:** Created automatically with each user
- **Naming:** Same as username
- **GID:** Matches UID
- **Members:** Only the user
- **Example:** User "john" has group "john"

#### 2. **System Groups**
- **Purpose:** For system services and processes
- **GID:** Low numbers (1-999)
- **Examples:** root, daemon, www-data, mysql

#### 3. **Regular Groups**
- **Purpose:** Created by administrators for user collaboration
- **GID:** 1000+
- **Examples:** developers, managers, students

#### 4. **Special Groups**
- **Purpose:** For specific permissions
- **Examples:** sudo, wheel, adm

---

### Creating and Deleting Groups

#### Creating Groups:
```bash
sudo groupadd [options] groupname
```

**Options:**
- `-g GID` — Specify group ID
- `-r` — Create system group (GID < 1000)

**Examples:**
```bash
# Create regular group
sudo groupadd developers

# Create system group
sudo groupadd -r myservice

# Create with specific GID
sudo groupadd -g 1500 projectteam
```

#### Deleting Groups:
```bash
sudo groupdel groupname
```

**Notes:**
- Cannot delete if it's a user's primary group
- Remove users from group first if needed

**Examples:**
```bash
sudo groupdel developers
```

---

### Modifying Groups

#### Changing Group Name:
```bash
sudo groupmod -n newname oldname
```

#### Changing Group ID:
```bash
sudo groupmod -g newGID groupname
```

**Examples:**
```bash
# Rename group
sudo groupmod -n engineers developers

# Change GID
sudo groupmod -g 2000 engineers
```

---

### Managing Group Memberships

#### Add User to Group:
```bash
sudo usermod -aG groupname username
# -a appends, -G specifies groups
```

#### Remove User from Group:
```bash
sudo gpasswd -d username groupname
```

#### Change User's Primary Group:
```bash
sudo usermod -g newprimarygroup username
```

#### Set Group Password:
```bash
sudo gpasswd groupname
# Allows users to use newgrp command
```

**Examples:**
```bash
# Add user to group
sudo usermod -aG developers john

# Remove user from group
sudo gpasswd -d john developers

# Change primary group
sudo usermod -g staff john

# Set group password
sudo gpasswd developers
```

---

### Viewing and Editing Group Information

#### View Group Information:
```bash
# Show user's groups
groups username
id username

# Show all groups
cat /etc/group

# Show specific group
getent group groupname
```

#### Edit Group Files Directly:
```bash
# Edit /etc/group (careful!)
sudo nano /etc/group

# Edit /etc/gshadow (very careful!)
sudo nano /etc/gshadow
```

**Better to use commands instead of direct editing!**

#### Check Group Membership:
```bash
# See who belongs to a group
getent group groupname

# See all groups a user belongs to
groups username
id username
```

---

## Hands-On Exercises for Students

1. **Password Management:**
   ```bash
   # Create test user
   sudo useradd -m testuser
   sudo passwd testuser
   
   # Check password status
   sudo passwd -S testuser
   
   # Force password change
   sudo passwd -e testuser
   ```

2. **Account Locking:**
   ```bash
   # Lock account
   sudo passwd -l testuser
   
   # Try to login (should fail)
   su testuser
   
   # Unlock account
   sudo passwd -u testuser
   ```

3. **Password Aging:**
   ```bash
   # Set password policies
   sudo chage -M 30 -W 7 testuser
   
   # Check settings
   sudo chage -l testuser
   ```

4. **Group Management:**
   ```bash
   # Create group
   sudo groupadd testgroup
   
   # Add user to group
   sudo usermod -aG testgroup testuser
   
   # Check membership
   groups testuser
   id testuser
   ```

5. **Advanced Group Operations:**
   ```bash
   # Change group name
   sudo groupmod -n newgroup testgroup
   
   # Remove user from group
   sudo gpasswd -d testuser newgroup
   
   # Delete group
   sudo groupdel newgroup
   ```

6. **Clean Up:**
   ```bash
   sudo userdel -r testuser
   ```

---

## Quick Reference Cheat-Sheet

### Password Commands:
- `passwd` — Change password
- `passwd -l/-u` — Lock/unlock account
- `passwd -e` — Expire password
- `passwd -S` — Show status

### Account Management:
- `chage -l` — List aging info
- `chage -M/-m/-W` — Set aging policies
- `chage -E` — Set expiration

### Group Commands:
- `groupadd group` — Create group
- `groupdel group` — Delete group
- `groupmod -n/-g` — Modify group
- `usermod -aG` — Add user to group
- `gpasswd -d` — Remove user from group

### View Information:
- `groups user` — Show user's groups
- `id user` — Show IDs and groups
- `getent group group` — Show group details

---

## Key Takeaways for Students

- Strong passwords and policies protect against attacks.
- Use chage for detailed password aging control.
- Groups enable efficient permission management.
- Always use commands over direct file editing.
- Test changes on non-production systems first!

Remember, security is an ongoing process. Regular audits and updates are essential!