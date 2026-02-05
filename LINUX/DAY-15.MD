# Day-15 ✅ Automation and Data Handling in Linux

## Introduction to Search and Filter Utilities

Search and filter utilities are essential tools in Linux for processing and analyzing text data.  
They allow DevOps engineers to efficiently locate, manipulate, and extract information from files and command outputs.

### 🔹 What Are Search and Filter Utilities?
- **Search**: Find specific patterns or content within files  
- **Filter**: Extract, sort, or modify data streams  
- **Process**: Handle large datasets and log files  
- **Automate**: Combine with scripts for data processing  

### 🔹 Common Use Cases
- Analyzing log files for errors  
- Extracting specific data from reports  
- Finding configuration issues  
- Processing large datasets  
- Automating data cleanup tasks  

---

## Importance of Searching and Filtering Data in Linux

In DevOps environments, searching and filtering is critical for:

### 🔹 System Administration
- **Log Analysis**: Quickly identify errors in system logs  
- **Configuration Management**: Find specific settings across files  
- **Troubleshooting**: Locate problematic processes or files  

### 🔹 Data Processing
- **Report Generation**: Extract relevant data from large files  
- **Data Cleaning**: Remove duplicates and sort information  
- **Automation**: Build scripts that process data automatically  

### 🔹 Security and Compliance
- **Audit Logs**: Search for security events  
- **Access Control**: Find unauthorized access attempts  
- **Compliance Checks**: Filter data for regulatory requirements  

### 🔹 Performance Benefits
- **Efficiency**: Process large files without loading everything into memory  
- **Speed**: Use pipes to chain commands for faster processing  
- **Scalability**: Handle growing data volumes in production systems  

---

## Overview of Key Utilities: grep, cat, sort, uniq

### 🔹 grep
- **Purpose**: Search for patterns in files or input streams  
- **Key Features**: Regular expressions, case-insensitive search, line numbers  
- **Use Case**: Find specific text in logs or code files  

### 🔹 cat
- **Purpose**: Concatenate and display file contents  
- **Key Features**: Display files, combine multiple files, show line numbers  
- **Use Case**: View file contents, create new files from input  

### 🔹 sort
- **Purpose**: Sort lines of text files or input streams  
- **Key Features**: Alphabetical/numerical sorting, reverse order, unique sorting  
- **Use Case**: Organize data, remove duplicates, prepare reports  

### 🔹 uniq
- **Purpose**: Remove duplicate lines from sorted input  
- **Key Features**: Show only unique lines, count occurrences, compare adjacent lines  
- **Use Case**: Clean data, identify duplicates, generate summaries  

### 🔹 Comparison Table

| Utility | Primary Function | Input Type | Output Type | Common Options |
|---------|------------------|------------|-------------|----------------|
| **grep** | Search patterns | Files/streams | Matching lines | `-i`, `-n`, `-v` |
| **cat** | Display/concatenate | Files | Combined output | `-n`, `-b`, `-s` |
| **sort** | Sort lines | Files/streams | Sorted output | `-r`, `-n`, `-k` |
| **uniq** | Remove duplicates | Sorted input | Unique lines | `-c`, `-d`, `-u` |

---

## Read Files Using cat, uniq, and sort

These utilities work together to read, process, and organize file contents.

### 🔹 Using cat to Read Files

#### Basic file reading:
```bash
cat file.txt
```
**Output:** Displays entire file content

#### Read multiple files:
```bash
cat file1.txt file2.txt
```
**Output:** Concatenates both files

#### Show line numbers:
```bash
cat -n file.txt
```
**Output:**
```
     1  First line
     2  Second line
     3  Third line
```

#### Suppress empty lines:
```bash
cat -s file.txt
```

---

### 🔹 Using sort to Organize Content

#### Basic alphabetical sort:
```bash
sort file.txt
```
**Output:** Lines sorted A-Z

#### Numerical sort:
```bash
sort -n numbers.txt
```
**Input:**
```
10
2
1
```
**Output:**
```
1
2
10
```

#### Reverse sort:
```bash
sort -r file.txt
```
**Output:** Z-A order

#### Sort by specific column:
```bash
sort -k 2 file.txt
```
**Sorts by second field (space/tab separated)**

#### Sort and remove duplicates:
```bash
sort -u file.txt
```
**Equivalent to `sort file.txt | uniq`**

---

### 🔹 Using uniq to Remove Duplicates

**Note:** `uniq` requires sorted input to work properly.

#### Remove duplicate lines:
```bash
sort file.txt | uniq
```
**Input:**
```
apple
banana
apple
cherry
```
**Output:**
```
apple
banana
cherry
```

#### Count occurrences:
```bash
sort file.txt | uniq -c
```
**Output:**
```
      2 apple
      1 banana
      1 cherry
```

#### Show only duplicates:
```bash
sort file.txt | uniq -d
```
**Output:**
```
apple
```

#### Show only unique lines:
```bash
sort file.txt | uniq -u
```
**Output:**
```
banana
cherry
```

---

### 🔹 Combining cat, sort, and uniq

#### Process a file: sort and remove duplicates
```bash
cat data.txt | sort | uniq
```

#### Count unique items in a file
```bash
cat names.txt | sort | uniq -c | sort -nr
```
**Output:** Most frequent names first

#### Find duplicate entries
```bash
cat log.txt | sort | uniq -d
```

---

## Introduction to the find Utility

`find` is a powerful command-line utility for searching files and directories based on various criteria.

### 🔹 Why Use find?
- **Locate Files**: Search by name, type, size, date, permissions  
- **Batch Operations**: Execute commands on found files  
- **System Administration**: Find old files, large files, specific types  
- **Automation**: Use in scripts for file management  

### 🔹 find vs Other Search Tools
- **locate**: Fast database search (requires updatedb)  
- **which**: Find executable files in PATH  
- **whereis**: Find binaries, sources, manuals  
- **find**: Comprehensive search with full control  

---

## Basic Syntax of find

### 🔹 Syntax Structure
```bash
find [path] [expression]
```

- **path**: Starting directory (default: current directory)  
- **expression**: Search criteria and actions  

### 🔹 Basic Examples

#### Find all files in current directory:
```bash
find .
```
**Output:** Lists all files and subdirectories recursively

#### Find files in specific directory:
```bash
find /home/user
```

#### Find files with specific name:
```bash
find . -name "file.txt"
```
**Output:** `./file.txt` (if found)

#### Case-insensitive name search:
```bash
find . -iname "FILE.txt"
```

---

## Advanced Usage and Filtering Options

### 🔹 Filtering by Type
```bash
find . -type f    # Files only
find . -type d    # Directories only
find . -type l    # Symbolic links only
```

### 🔹 Filtering by Name Patterns
```bash
find . -name "*.txt"        # Exact match
find . -iname "*.TXT"       # Case-insensitive
find . -name "*report*"     # Contains "report"
```

### 🔹 Filtering by Size
```bash
find . -size +100M          # Larger than 100MB
find . -size -1k            # Smaller than 1KB
find . -size 10M            # Exactly 10MB
```

### 🔹 Filtering by Time
```bash
find . -mtime -7            # Modified in last 7 days
find . -mtime +30           # Modified more than 30 days ago
find . -mtime 7             # Modified exactly 7 days ago
```

**Time Options:**
- `-mtime`: Modified time (days)  
- `-atime`: Access time  
- `-ctime`: Change time  

### 🔹 Filtering by Permissions
```bash
find . -perm 755            # Exact permissions
find . -perm -4000          # Has setuid bit
find . -perm /111           # Executable by someone
```

### 🔹 Combining Filters with Operators
```bash
find . -name "*.log" -mtime -7    # AND (both conditions)
find . -name "*.tmp" -o -name "*.bak"    # OR
find . -not -name "*.txt"        # NOT
```

### 🔹 Limiting Depth
```bash
find . -maxdepth 2 -name "*.txt"    # Search only 2 levels deep
find . -mindepth 1 -type f          # Skip current directory
```

---

## Practical Examples of Finding Files by Name, Type, Size, and Modification Date

### 🔹 By Name

#### Find all .txt files:
```bash
find /home -name "*.txt"
```

#### Find files starting with "config":
```bash
find . -name "config*"
```

#### Find files with case-insensitive extension:
```bash
find . -iname "*.JPG"
```

#### Find files containing "backup" in name:
```bash
find . -name "*backup*"
```

---

### 🔹 By Type

#### Find all regular files:
```bash
find . -type f
```

#### Find all directories:
```bash
find . -type d
```

#### Find all symbolic links:
```bash
find . -type l
```

#### Find all executable files:
```bash
find . -type f -executable
```

---

### 🔹 By Size

#### Find files larger than 1GB:
```bash
find . -type f -size +1G
```

#### Find files smaller than 100KB:
```bash
find . -type f -size -100k
```

#### Find files exactly 1MB:
```bash
find . -type f -size 1M
```

#### Find largest files in directory:
```bash
find . -type f -exec ls -lh {} \; | sort -k5 -hr | head -10
```

---

### 🔹 By Modification Date

#### Find files modified in last 24 hours:
```bash
find . -type f -mtime -1
```

#### Find files modified more than 30 days ago:
```bash
find . -type f -mtime +30
```

#### Find files modified between 7-14 days ago:
```bash
find . -type f -mtime +7 -mtime -14
```

#### Find files accessed in last hour:
```bash
find . -type f -amin -60
```

#### Find recently modified config files:
```bash
find /etc -name "*.conf" -mtime -7
```

---

### 🔹 Advanced Practical Examples

#### Find and delete old log files:
```bash
find /var/log -name "*.log" -mtime +30 -delete
```

#### Find large files and get their sizes:
```bash
find . -type f -size +100M -exec ls -lh {} \;
```

#### Find files owned by specific user:
```bash
find . -user rajat
```

#### Find files with specific permissions:
```bash
find . -perm 644
```

#### Find empty files and directories:
```bash
find . -empty
```

#### Find and compress old files:
```bash
find . -type f -mtime +365 -exec gzip {} \;
```

---

## ⭐ Real-World DevOps Scenarios

### 🔸 Scenario 1: Log Analysis
```bash
# Find error logs from last 24 hours
find /var/log -name "*.log" -mtime -1 -exec grep -l "ERROR" {} \;

# Count errors by type
find /var/log -name "*.log" -exec grep "ERROR" {} \; | sort | uniq -c
```

### 🔸 Scenario 2: Disk Cleanup
```bash
# Find large temporary files
find /tmp -type f -size +100M

# Remove old cache files
find ~/.cache -type f -mtime +30 -delete

# Archive old logs
find /var/log -name "*.log" -mtime +7 -exec tar -czf {}.tar.gz {} \; -exec rm {} \;
```

### 🔸 Scenario 3: Code Quality Check
```bash
# Find Python files with syntax errors
find . -name "*.py" -exec python -m py_compile {} \; 2>&1 | grep -v "SyntaxError"

# Find large source files
find . -name "*.py" -size +1M
```

### 🔸 Scenario 4: Security Audit
```bash
# Find world-writable files
find /home -type f -perm -002

# Find files modified recently (potential compromise)
find /etc -type f -mtime -1

# Find executable files in user directories
find /home -type f -executable
```

---

## 🎯 Key Takeaways

✅ **grep** searches for patterns in text  
✅ **cat** displays and concatenates files  
✅ **sort** organizes lines alphabetically/numerically  
✅ **uniq** removes duplicates from sorted input  
✅ **find** locates files by name, type, size, date, permissions  
✅ Combine utilities with pipes for powerful data processing  
✅ Use `-exec` with find to perform actions on found files  
✅ Always test find commands before using `-delete`  

---

## 📝 Quick Reference: Search and Filter Commands

```bash
# GREP - Search Patterns
grep "pattern" file.txt              # Basic search
grep -i "pattern" file.txt           # Case-insensitive
grep -n "pattern" file.txt           # Show line numbers
grep -v "pattern" file.txt           # Invert match
grep -r "pattern" /path/             # Recursive search

# CAT - Display Files
cat file.txt                         # Display file
cat -n file.txt                      # With line numbers
cat file1.txt file2.txt > combined.txt  # Concatenate

# SORT - Sort Lines
sort file.txt                        # Alphabetical sort
sort -n numbers.txt                  # Numerical sort
sort -r file.txt                     # Reverse sort
sort -k 2 file.txt                   # Sort by column 2
sort -u file.txt                     # Unique sort

# UNIQ - Remove Duplicates
uniq file.txt                        # Remove duplicates
uniq -c file.txt                     # Count occurrences
uniq -d file.txt                     # Show duplicates only
uniq -u file.txt                     # Show unique only

# FIND - Locate Files
find . -name "*.txt"                 # By name
find . -type f                       # Files only
find . -type d                       # Directories only
find . -size +1M                     # Larger than 1MB
find . -mtime -7                     # Modified last 7 days
find . -perm 755                     # Specific permissions
find . -exec ls -l {} \;             # Execute command on results
```

---

## 🚨 Common Issues & Troubleshooting

### 🔹 find Not Finding Files
- Check permissions on directories  
- Use absolute paths  
- Verify file actually exists  

### 🔹 grep No Results
- Check case sensitivity (`-i` flag)  
- Use word boundaries (`\<word\>`)  
- Check if file has content  

### 🔹 sort Not Working as Expected
- Use `-n` for numerical sorting  
- Specify key with `-k` for column sorting  
- Check locale settings  

### 🔹 uniq Not Removing Duplicates
- Input must be sorted first  
- Use `sort | uniq`  

---

## 📚 Further Reading
- `man grep`, `man find`, `man sort`  
- Regular expressions guide  
- Advanced find command tutorials  
      