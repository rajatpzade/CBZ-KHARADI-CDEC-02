# Day-14

---

## Automation and Data Handling in Linux

Welcome to Day 14! Today, we'll explore essential Linux skills for automation and data handling: archiving and compression for efficient data management, and cron jobs for automating routine tasks. These tools are crucial for backups, system maintenance, and productivity in Linux environments.

---

### Overview of Archiving

**What is Archiving?**
Archiving combines multiple files and directories into a single file (archive) for easier storage, transfer, and organization. Unlike compression, archiving doesn't reduce file size but bundles files together.

**Why Archive Files?**
- **Organization:** Group related files into one package
- **Backup:** Create snapshots of data for recovery
- **Transfer:** Send multiple files as one unit
- **Storage:** Efficiently store collections of files

**Archiving vs. Compression:**
- **Archiving:** Bundles files (e.g., tar)
- **Compression:** Reduces file size (e.g., gzip)
- **Combined:** Archive then compress for best results

---

### Common Use Cases: Backups, Data Transfer, Organization

#### 1. **Backups**
- Create archives of important data for disaster recovery
- Schedule automated backups using cron
- Store archives on external drives or cloud storage

#### 2. **Data Transfer**
- Bundle files for sending via email or network
- Reduce transfer time by archiving before sending
- Preserve file permissions and metadata

#### 3. **Organization**
- Group project files into archives
- Archive old data for long-term storage
- Create distributable packages for software

**Examples:**
- Backup home directory: `tar -czf backup.tar.gz /home/user`
- Transfer project: `tar -cf project.tar project/`
- Organize logs: `tar -czf logs.tar.gz /var/log/`

---

### Creating and Extracting Archives with tar

`tar` (Tape Archive) is the standard Linux archiving tool.

#### Basic tar Syntax:
```bash
tar [options] [archive-name] [files/directories]
```

#### Creating Archives:
```bash
# Create uncompressed archive
tar -cf archive.tar file1 file2 directory/

# Create compressed archive (gzip)
tar -czf archive.tar.gz file1 file2 directory/

# Create compressed archive (bzip2)
tar -cjf archive.tar.bz2 file1 file2 directory/

# Create compressed archive (xz)
tar -cJf archive.tar.xz file1 file2 directory/
```

#### Extracting Archives:
```bash
# Extract uncompressed archive
tar -xf archive.tar

# Extract compressed archive (auto-detects format)
tar -xf archive.tar.gz
tar -xf archive.tar.bz2
tar -xf archive.tar.xz

# Extract to specific directory
tar -xf archive.tar -C /path/to/directory/

# Extract specific files
tar -xf archive.tar file1.txt
```

#### Common Options:
- `-c` — Create archive
- `-x` — Extract archive
- `-f` — Specify filename
- `-z` — Use gzip compression
- `-j` — Use bzip2 compression
- `-J` — Use xz compression
- `-v` — Verbose output
- `-t` — List archive contents
- `-C` — Change to directory

---

### Managing Archive Contents

#### Listing Archive Contents:
```bash
# List files in archive
tar -tf archive.tar

# List with details
tar -tvf archive.tar
```

#### Adding Files to Existing Archive:
```bash
# Append files (uncompressed archives only)
tar -rf archive.tar newfile.txt

# For compressed archives, extract, add, re-compress
tar -xf archive.tar.gz
tar -czf archive.tar.gz original/ newfile.txt
```

#### Verifying Archives:
```bash
# Compare archive with filesystem
tar -df archive.tar

# Test archive integrity
tar -tf archive.tar > /dev/null
```

---

### Introduction to Compression

**What is Compression?**
Compression reduces file size by encoding data more efficiently, making files smaller for storage and transfer.

**Why Compress Files?**
- **Save Storage Space:** Reduce disk usage
- **Faster Transfers:** Smaller files transfer quicker
- **Backup Efficiency:** Store more data in less space
- **Archive Optimization:** Combine with archiving for best results

---

### The Role of Compression in Reducing File Sizes

Compression algorithms identify patterns in data and represent them more efficiently. Different file types compress differently:

- **Text Files:** High compression (80-90% reduction)
- **Images/Audio/Video:** Low compression (already compressed)
- **Executables:** Moderate compression (50-70% reduction)

**Compression Trade-offs:**
- **Pros:** Smaller files, faster transfers
- **Cons:** CPU usage during compression/decompression, slight data loss in lossy compression

---

### Differences Between Compression Formats (e.g., gzip, bzip2, xz)

| Format | Tool | Compression Ratio | Speed | Use Case |
|--------|------|-------------------|-------|----------|
| **gzip** | gzip/gunzip | Good | Fast | General purpose, web content |
| **bzip2** | bzip2/bunzip2 | Better | Slower | High compression, archives |
| **xz** | xz/unxz | Best | Slowest | Maximum compression, large files |

**Choosing a Format:**
- **gzip:** Fast, widely supported, good for everyday use
- **bzip2:** Better compression than gzip, good for backups
- **xz:** Best compression, use for large archives where size matters most

---

### Using gzip and gunzip

**gzip** compresses files, **gunzip** decompresses them.

#### Compressing Files:
```bash
# Compress single file
gzip file.txt                    # Creates file.txt.gz

# Compress with different compression levels
gzip -1 file.txt                 # Fast compression
gzip -9 file.txt                 # Best compression

# Keep original file
gzip -c file.txt > file.txt.gz   # -c outputs to stdout
```

#### Decompressing Files:
```bash
# Decompress file
gunzip file.txt.gz               # Creates file.txt

# Decompress to stdout
gunzip -c file.txt.gz            # View compressed file

# Test compressed file
gunzip -t file.txt.gz            # Check integrity
```

#### Working with Multiple Files:
```bash
# Compress all .txt files
gzip *.txt

# Compress recursively
gzip -r directory/
```

---

### Using bzip2 and bunzip2

**bzip2** offers better compression than gzip but is slower.

#### Compressing Files:
```bash
# Compress file
bzip2 file.txt                   # Creates file.txt.bz2

# Compress with options
bzip2 -9 file.txt                # Maximum compression
bzip2 -c file.txt > file.txt.bz2 # Keep original
```

#### Decompressing Files:
```bash
# Decompress file
bunzip2 file.txt.bz2             # Creates file.txt

# Decompress to stdout
bunzip2 -c file.txt.bz2

# Test integrity
bunzip2 -t file.txt.bz2
```

---

### Using xz and unxz

**xz** provides the best compression but is the slowest.

#### Compressing Files:
```bash
# Compress file
xz file.txt                      # Creates file.txt.xz

# Compress with options
xz -9 file.txt                   # Maximum compression
xz -c file.txt > file.txt.xz     # Keep original
```

#### Decompressing Files:
```bash
# Decompress file
unxz file.txt.xz                 # Creates file.txt

# Decompress to stdout
unxz -c file.txt.xz

# Test integrity
unxz -t file.txt.xz
```

---

### Combining Archiving and Compression

The most efficient approach: archive first, then compress.

#### Best Practices:
```bash
# Create compressed archive (recommended)
tar -czf archive.tar.gz files/    # gzip
tar -cjf archive.tar.bz2 files/   # bzip2
tar -cJf archive.tar.xz files/    # xz

# Extract compressed archive
tar -xzf archive.tar.gz           # Auto-detects compression
tar -xjf archive.tar.bz2
tar -xJf archive.tar.xz
```

**Why Combine?**
- Archive preserves file structure and permissions
- Compression reduces size
- Single file for easy management

---

### Practical: Compressing Files with tar, gzip, bzip2, xz

#### Examples:
```bash
# Backup home directory with gzip
tar -czf home_backup.tar.gz /home/user

# Compress project with bzip2
tar -cjf project.tar.bz2 project/

# Archive logs with xz
tar -cJf logs.tar.xz /var/log/

# Compress single file with gzip
gzip important_file.txt

# Compress with bzip2
bzip2 large_file.iso
```

---

### Practical: Decompressing Files with tar, gunzip, bunzip2, unxz

#### Examples:
```bash
# Extract backup
tar -xzf home_backup.tar.gz

# Extract to specific location
tar -xzf project.tar.bz2 -C /tmp/

# Decompress single file
gunzip important_file.txt.gz

# Decompress bzip2 file
bunzip2 large_file.iso.bz2

# Decompress xz file
unxz logs.tar.xz
```

---

### Introduction to CronTab

**What is Cron?**
Cron is a time-based job scheduler in Linux. It runs commands or scripts at specified times/dates automatically.

**What is Crontab?**
Crontab is the file that contains cron jobs for a user. Each user can have their own crontab.

**Why Use Cron?**
- **Automation:** Run tasks without manual intervention
- **Scheduling:** Execute commands at specific times
- **Maintenance:** Automate backups, updates, cleanup
- **Monitoring:** Run checks periodically

---

### Understanding The CronTab Syntax

#### Basic Crontab Format:
```
* * * * * command
│ │ │ │ │
│ │ │ │ └─ Day of week (0-7, 0/7=Sunday)
│ │ │ └─── Month (1-12)
│ │ └───── Day of month (1-31)
│ └─────── Hour (0-23)
└───────── Minute (0-59)
```

#### Special Characters:
- `*` — Any value
- `,` — List of values (e.g., 1,3,5)
- `-` — Range of values (e.g., 1-5)
- `/` — Step values (e.g., */2 = every 2 units)

#### Examples:
```bash
# Run every minute
* * * * * /path/to/script.sh

# Run at 2:30 AM daily
30 2 * * * /path/to/backup.sh

# Run every Monday at 9 AM
0 9 * * 1 /path/to/report.sh

# Run every 15 minutes
*/15 * * * * /path/to/check.sh

# Run on 1st of every month at midnight
0 0 1 * * /path/to/monthly.sh
```

---

### Creating and Managing Cron Jobs

#### Viewing Crontab:
```bash
# View current user's crontab
crontab -l

# View specific user's crontab (root only)
crontab -u username -l
```

#### Editing Crontab:
```bash
# Edit current user's crontab
crontab -e

# Edit specific user's crontab (root only)
crontab -u username -e
```

#### Adding Jobs:
```bash
# Open crontab editor
crontab -e

# Add these lines:
# Backup home directory daily at 2 AM
0 2 * * * tar -czf /backup/home_$(date +\%Y\%m\%d).tar.gz /home/user

# Update system weekly on Sundays at 3 AM
0 3 * * 0 apt update && apt upgrade -y

# Clean temp files hourly
0 * * * * rm -rf /tmp/*.tmp
```

#### Removing Jobs:
```bash
# Remove all jobs
crontab -r

# Remove specific user's jobs (root only)
crontab -u username -r

# Confirm before removing
crontab -i -r
```

#### Managing Cron Service:
```bash
# Check cron status
systemctl status cron

# Start cron
sudo systemctl start cron

# Stop cron
sudo systemctl stop cron

# Restart cron
sudo systemctl restart cron
```

---

### Automating Routine Tasks like Backups, System Updates, and Cleanup Scripts

#### 1. **Automated Backups**
```bash
# Daily backup of important directories
0 2 * * * tar -czf /backup/daily_$(date +\%Y\%m\%d).tar.gz /home /etc /var/www

# Weekly full backup
0 3 * * 0 rsync -av /home /backup/weekly/
```

#### 2. **System Updates**
```bash
# Update package lists daily
0 1 * * * apt update

# Upgrade packages weekly
0 2 * * 0 apt upgrade -y

# Clean package cache weekly
0 3 * * 0 apt autoremove && apt autoclean
```

#### 3. **Cleanup Scripts**
```bash
# Clean temporary files hourly
0 * * * * find /tmp -type f -mtime +1 -delete

# Rotate logs weekly
0 4 * * 0 logrotate /etc/logrotate.conf

# Clean old backups monthly (keep last 30 days)
0 5 1 * * find /backup -name "*.tar.gz" -mtime +30 -delete
```

#### 4. **Monitoring Tasks**
```bash
# Check disk space daily
0 6 * * * df -h | mail -s "Daily Disk Report" admin@example.com

# Monitor services every 5 minutes
*/5 * * * * systemctl is-active apache2 || systemctl restart apache2
```

---

## Hands-On Exercises for Students

1. **Archiving Practice:**
   ```bash
   # Create test files
   mkdir test_archive
   echo "Hello World" > test_archive/file1.txt
   echo "Linux is awesome" > test_archive/file2.txt
   
   # Create archive
   tar -cf test.tar test_archive/
   
   # List contents
   tar -tf test.tar
   
   # Extract archive
   tar -xf test.tar -C /tmp/
   ```

2. **Compression Practice:**
   ```bash
   # Compress with different formats
   gzip test_archive/file1.txt
   bzip2 test_archive/file2.txt
   xz test_archive/file3.txt
   
   # Check sizes
   ls -lh test_archive/
   
   # Decompress
   gunzip file1.txt.gz
   bunzip2 file2.txt.bz2
   unxz file3.txt.xz
   ```

3. **Combined Archiving and Compression:**
   ```bash
   # Create compressed archive
   tar -czf backup.tar.gz test_archive/
   
   # Extract and verify
   tar -tzf backup.tar.gz
   tar -xzf backup.tar.gz -C /tmp/
   ```

4. **Cron Job Setup:**
   ```bash
   # View current crontab
   crontab -l
   
   # Edit crontab (add these lines)
   crontab -e
   
   # Add:
   # * * * * * echo "Hello from cron" >> /tmp/cron_test.log
   # 0 * * * * date >> /tmp/hourly.log
   
   # Wait and check logs
   cat /tmp/cron_test.log
   cat /tmp/hourly.log
   ```

5. **Advanced Automation:**
   ```bash
   # Create backup script
   nano ~/backup.sh
   # Add: tar -czf /tmp/backup_$(date +%Y%m%d).tar.gz /home/user/Documents
   
   # Make executable
   chmod +x ~/backup.sh
   
   # Add to crontab for daily backup
   crontab -e
   # Add: 0 2 * * * /home/user/backup.sh
   ```

---

## Quick Reference Cheat-Sheet

### Archiving with tar:
- `tar -cf archive.tar files/` — Create archive
- `tar -xf archive.tar` — Extract archive
- `tar -czf archive.tar.gz files/` — Create gzip archive
- `tar -cjf archive.tar.bz2 files/` — Create bzip2 archive
- `tar -cJf archive.tar.xz files/` — Create xz archive
- `tar -tf archive.tar` — List contents

### Compression:
- `gzip file` / `gunzip file.gz` — gzip compression
- `bzip2 file` / `bunzip2 file.bz2` — bzip2 compression
- `xz file` / `unxz file.xz` — xz compression

### Cron Jobs:
- `crontab -l` — List jobs
- `crontab -e` — Edit jobs
- `* * * * * command` — Run every minute
- `0 2 * * * command` — Run daily at 2 AM
- `0 9 * * 1 command` — Run Mondays at 9 AM

### Common Cron Schedules:
- `@hourly` — Every hour
- `@daily` — Every day
- `@weekly` — Every week
- `@monthly` — Every month

---

## Key Takeaways for Students

- Archiving bundles files; compression reduces size; combine both for efficiency.
- tar is the standard archiver; gzip/bzip2/xz for compression.
- Cron automates tasks: use crontab -e to schedule jobs.
- Always test cron jobs manually before scheduling.
- Backup critical data regularly using automated scripts.

Remember, automation saves time and prevents errors. Start with simple cron jobs and build up to complex automation!
