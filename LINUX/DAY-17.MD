# Day-16 ✅ Managing Processes and Optimizing Performance

## Introduction to Processes

A **process** is a running instance of a program in Linux. Every time you run a command or application, it creates one or more processes.

### 🔹 What is a Process?
- **Program in Execution**: Code + data + resources  
- **Independent Entity**: Each process has its own memory space  
- **Managed by Kernel**: OS schedules and controls processes  
- **Has Unique ID**: Process ID (PID) identifies each process  

### 🔹 Why Manage Processes?
- **Resource Allocation**: CPU, memory, I/O  
- **System Stability**: Prevent runaway processes  
- **Performance Monitoring**: Identify bottlenecks  
- **Troubleshooting**: Debug hanging applications  
- **Automation**: Control background tasks  

### 🔹 Process Lifecycle
1. **Creation**: Fork from parent process  
2. **Execution**: Running state  
3. **Termination**: Normal exit or kill  
4. **Cleanup**: Resources freed by kernel  

---

## Types of Processes and Jobs

### 🔹 Types of Processes

#### 1. **Foreground Processes**
- **Interactive**: Run in terminal, user waits for completion  
- **Examples**: `ls`, `nano`, `gcc compile.c`  
- **Control**: User can interrupt with Ctrl+C  

#### 2. **Background Processes**
- **Non-Interactive**: Run independently of terminal  
- **Examples**: Web servers, daemons, long-running scripts  
- **Control**: Continue running after terminal closes  

#### 3. **Parent and Child Processes**
- **Parent**: Creates child processes (e.g., shell creates `ls`)  
- **Child**: Inherits properties from parent  
- **Relationship**: PPID (Parent Process ID)  

#### 4. **Orphan Processes**
- **Parent Died**: Child process continues running  
- **Adopted**: Init process (PID 1) becomes new parent  

#### 5. **Zombie Processes**
- **Terminated**: Process finished but entry remains  
- **Waiting**: Parent hasn't collected exit status  
- **Cleanup**: Parent calls `wait()` or exits  

---

### 🔹 Types of Jobs

#### 1. **Foreground Jobs**
- **Active**: Currently controlling terminal  
- **Input/Output**: Connected to terminal  
- **Examples**: Editing file with `vim`  

#### 2. **Background Jobs**
- **Running**: No terminal control  
- **Output**: May redirect to files  
- **Examples**: `find / -name "*.log" > logs.txt &`  

#### 3. **Stopped Jobs**
- **Paused**: Suspended execution  
- **Resume**: Can be continued later  
- **Examples**: Ctrl+Z stops foreground job  

---

## Basic Process Management Commands

### 🔹 Viewing Processes

#### `ps` Command
```bash
ps              # Current shell processes
ps aux          # All processes with details
ps -ef          # Full listing
ps -p 1234      # Specific PID
```

#### `top` Command
```bash
top             # Real-time process monitor
top -u username # User's processes
```

#### `htop` Command (if installed)
```bash
htop            # Enhanced interactive top
```

---

### 🔹 Controlling Processes

#### `kill` Command
```bash
kill 1234               # Send SIGTERM to PID 1234
kill -9 1234            # Force kill (SIGKILL)
kill -STOP 1234         # Stop process
kill -CONT 1234         # Continue stopped process
```

#### `killall` Command
```bash
killall firefox         # Kill all firefox processes
killall -9 apache2      # Force kill all apache processes
```

#### `pkill` Command
```bash
pkill -f "python script" # Kill by pattern
pkill -u rajat          # Kill user's processes
```

---

### 🔹 Process Priority

#### `nice` Command
```bash
nice -n 10 command      # Start with lower priority
nice command            # Default nice value
```

#### `renice` Command
```bash
renice -n 5 -p 1234     # Change priority of PID 1234
renice -n -10 -u rajat  # Change all user's processes
```

---

## Understanding Process States

Processes can be in different states during their lifecycle.

### 🔹 Process States

| State | Code | Description |
|-------|------|-------------|
| **Running** | R | Currently executing on CPU |
| **Sleeping** | S | Waiting for event (interruptible) |
| **Waiting** | D | Uninterruptible sleep (usually I/O) |
| **Stopped** | T | Stopped by job control signal |
| **Zombie** | Z | Terminated, waiting for parent |

### 🔹 State Transitions
- **New → Ready**: Process created, waiting for CPU  
- **Ready → Running**: Scheduled by kernel  
- **Running → Waiting**: Needs I/O or event  
- **Waiting → Ready**: Event occurred  
- **Running → Terminated**: Process exits  

### 🔹 Viewing States
```bash
ps aux | head -10
# Look at STAT column: R, S, D, T, Z
```

---

## Job Control Basics

Job control allows managing multiple processes in a shell session.

### 🔹 Job Control Commands

#### Background Jobs
```bash
command &               # Start in background
jobs                    # List jobs
fg %1                   # Bring job 1 to foreground
bg %1                   # Send job 1 to background
```

#### Stopping and Resuming
```bash
Ctrl+Z                  # Stop foreground job
fg                      # Resume in foreground
bg                      # Resume in background
```

#### Job Management
```bash
jobs -l                 # List jobs with PIDs
kill %1                 # Kill job 1
disown %1               # Remove from job list
```

---

### 🔹 Job States

| State | Description |
|-------|-------------|
| **Running** | Active in foreground/background |
| **Stopped** | Suspended (Ctrl+Z) |
| **Done** | Completed successfully |
| **Terminated** | Killed or exited with error |

---

## Understanding Process and Thread Management

### 🔹 Processes vs Threads

#### Processes
- **Heavyweight**: Separate memory space  
- **Independent**: Fault isolation  
- **Communication**: IPC (pipes, sockets, shared memory)  
- **Creation**: `fork()` system call  

#### Threads
- **Lightweight**: Shared memory space  
- **Dependent**: Within process  
- **Communication**: Direct memory access  
- **Creation**: `pthread_create()`  

### 🔹 Process Hierarchy
- **Init (PID 1)**: Root of process tree  
- **Systemd**: Modern init system  
- **Parent-Child**: Tree structure  
- **Sessions**: Group related processes  

### 🔹 Thread Management
- **Kernel Threads**: Managed by OS  
- **User Threads**: Library-managed  
- **Scheduling**: Kernel schedules threads  
- **Synchronization**: Mutexes, semaphores  

---

## Exploring with ps Command

`ps` (process status) displays information about processes.

### 🔹 Basic Usage
```bash
ps              # Current shell processes
```

### 🔹 Common Options

#### Standard Syntax
```bash
ps [options]
```

#### BSD Style (no dash)
```bash
ps aux          # All processes, user-oriented
ps ax           # All processes, no headers
ps u            # User-oriented format
```

#### UNIX Style (with dash)
```bash
ps -e           # All processes
ps -f           # Full format
ps -l           # Long format
ps -p 123,456   # Specific PIDs
```

---

### 🔹 Output Fields

| Field | Description |
|-------|-------------|
| **PID** | Process ID |
| **PPID** | Parent Process ID |
| **USER** | Owner username |
| **%CPU** | CPU usage percentage |
| **%MEM** | Memory usage percentage |
| **VSZ** | Virtual memory size (KB) |
| **RSS** | Resident set size (KB) |
| **TTY** | Controlling terminal |
| **STAT** | Process state |
| **START** | Start time |
| **TIME** | CPU time used |
| **COMMAND** | Command with arguments |

---

### 🔹 Practical Examples

#### View all processes
```bash
ps aux
```

#### Find specific process
```bash
ps aux | grep nginx
```

#### Process tree
```bash
ps -ejH          # Show process hierarchy
ps f             # ASCII art process tree
```

#### Memory usage
```bash
ps aux --sort=-%mem | head
```

#### CPU usage
```bash
ps aux --sort=-%cpu | head
```

#### User's processes
```bash
ps -u rajat
```

---

## Real-Time Monitoring with top

`top` provides real-time system monitoring and process management.

### 🔹 Starting top
```bash
top             # Default view
top -u username # User's processes
top -p 123,456  # Specific PIDs
```

### 🔹 top Interface

#### Header Information
```
top - 14:25:30 up 5 days,  3:45,  2 users,  load average: 0.15, 0.08, 0.06
Tasks: 123 total,   1 running, 122 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.5 us,  1.2 sy,  0.0 ni, 96.2 id,  0.0 wa,  0.0 hi,  0.1 si,  0.0 st
MiB Mem :   7946.0 total,   2345.6 free,   3456.7 used,   2143.7 buff/cache
MiB Swap:   2048.0 total,   1800.0 free,    248.0 used.   4123.4 avail Mem
```

#### Process List
```
  PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
 1234 rajat     20   0  456789  23456   7890 S   5.0   0.3   1:23.45 firefox
 5678 apache    20   0  123456   7890   2345 S   2.1   0.1   0:45.67 httpd
```

---

### 🔹 Interactive Commands

| Key | Action |
|-----|--------|
| **h** | Help |
| **q** | Quit |
| **k** | Kill process |
| **r** | Renice process |
| **Space** | Refresh |
| **M** | Sort by memory |
| **P** | Sort by CPU |
| **T** | Sort by time |
| **u** | Filter by user |
| **c** | Show command line |
| **1** | Show all CPUs |

---

### 🔹 Customizing top

#### Configuration File
```bash
~/.toprc        # User configuration
```

#### Command Line Options
```bash
top -d 5        # Update every 5 seconds
top -n 10       # Exit after 10 iterations
top -b          # Batch mode (for scripts)
```

---

## Analyzing Performance Metrics

### 🔹 CPU Metrics

#### Load Average
- **1-minute, 5-minute, 15-minute averages**  
- **Rule of Thumb**: < 1.0 per CPU core is good  
- **Check**: `uptime` or `cat /proc/loadavg`  

#### CPU Utilization
- **User Time**: Application code  
- **System Time**: Kernel operations  
- **Idle Time**: Available CPU  
- **I/O Wait**: Disk/network waiting  

---

### 🔹 Memory Metrics

#### Memory Types
- **Physical RAM**: Hardware memory  
- **Virtual Memory**: RAM + Swap  
- **Resident Memory**: Actually in RAM  
- **Shared Memory**: Libraries, shared segments  

#### Memory Usage
```bash
free -h         # Human readable
vmstat 1        # Virtual memory stats
```

---

### 🔹 I/O Metrics

#### Disk I/O
```bash
iostat -x 1     # Extended I/O stats
iotop           # Real-time I/O monitor
```

#### Network I/O
```bash
iptraf          # Network traffic monitor
nload           # Network load monitor
```

---

### 🔹 System Performance Tools

#### `vmstat`
```bash
vmstat 1        # Virtual memory stats every second
```

#### `iostat`
```bash
iostat -c 1     # CPU stats
iostat -d 1     # Disk stats
```

#### `sar`
```bash
sar -u 1        # CPU usage history
sar -r 1        # Memory usage history
```

#### `perf`
```bash
perf stat command   # Performance counters
perf top            # System-wide profiling
```

---

## ⭐ Real-World DevOps Scenarios

### 🔸 Scenario 1: Troubleshoot High CPU Usage
```bash
# Check load average
uptime

# Find CPU-intensive processes
ps aux --sort=-%cpu | head

# Monitor in real-time
top

# Kill problematic process
kill -9 <PID>
```

---

### 🔸 Scenario 2: Memory Leak Investigation
```bash
# Check memory usage
free -h

# Find memory-hungry processes
ps aux --sort=-%mem | head

# Monitor memory over time
vmstat 1

# Check for OOM kills
dmesg | grep -i oom
```

---

### 🔸 Scenario 3: Background Job Management
```bash
# Start backup in background
tar -czf backup.tar.gz /data &

# Check job status
jobs

# Monitor progress
ps aux | grep tar

# Bring to foreground if needed
fg %1
```

---

### 🔸 Scenario 4: Process Priority Tuning
```bash
# Check current priorities
ps -eo pid,ppid,pri,ni,comm

# Lower priority of CPU-intensive task
renice -n 10 -p <PID>

# Start with low priority
nice -n 19 ./cpu-intensive-script &
```

---

### 🔸 Scenario 5: Zombie Process Cleanup
```bash
# Find zombie processes
ps aux | awk '{print $8}' | grep -c Z

# Identify zombie parents
ps -eo pid,ppid,stat,cmd | grep Z

# Kill parent process
kill -9 <PPID>
```

---

## 🎯 Key Takeaways

✅ **Process**: Running instance of a program with unique PID  
✅ **ps aux**: View all processes with details  
✅ **top**: Real-time monitoring and process management  
✅ **kill -9**: Force terminate unresponsive processes  
✅ **nice/renice**: Control process scheduling priority  
✅ **Jobs**: Foreground/background process groups  
✅ **States**: R (running), S (sleeping), D (waiting), T (stopped), Z (zombie)  
✅ **Load Average**: System load indicator (< 1.0 per core is good)  
✅ **Memory**: Monitor RSS, VSZ, and swap usage  
✅ **I/O**: Use iostat and iotop for disk/network monitoring  

---

## 📝 Quick Reference: Process Management Commands

```bash
# VIEW PROCESSES
ps aux                          # All processes
ps -ef                          # Full listing
ps -p 1234                      # Specific PID
ps -u rajat                     # User's processes
top                             # Real-time monitor
htop                            # Enhanced top

# CONTROL PROCESSES
kill 1234                       # Terminate PID
kill -9 1234                    # Force kill
killall firefox                 # Kill by name
pkill -f "script.py"            # Kill by pattern

# PRIORITY MANAGEMENT
nice -n 10 command              # Start with priority
renice -n 5 -p 1234             # Change priority

# JOB CONTROL
command &                       # Background job
jobs                            # List jobs
fg %1                           # Foreground job
bg %1                           # Background job
Ctrl+Z                          # Stop job

# PERFORMANCE MONITORING
vmstat 1                        # Memory stats
iostat -x 1                     # I/O stats
sar -u 1                        # CPU history
free -h                         # Memory usage
uptime                          # Load average
```

---

## 🚨 Common Issues & Troubleshooting

### 🔹 Process Won't Die
- Try `kill` first (SIGTERM)  
- Use `kill -9` (SIGKILL) as last resort  
- Check if process is in D state (uninterruptible)  

### 🔹 High CPU Usage
- Identify with `top` or `ps aux --sort=-%cpu`  
- Check for infinite loops in code  
- Consider nice values for non-critical processes  

### 🔹 Memory Issues
- Use `free -h` to check available memory  
- Look for memory leaks with `valgrind`  
- Consider adding swap space  

### 🔹 Zombie Processes
- Zombies are harmless but indicate parent issues  
- Kill parent process to clean up  
- Check application code for proper child handling  

### 🔹 Load Average High
- Compare to CPU cores (`nproc`)  
- Identify bottleneck (CPU, memory, I/O)  
- Use `sar` for historical data  

---

## 📚 Further Reading
- `man ps`, `man top`, `man kill`  
- Linux process scheduling  
- System performance tuning guides  
- Advanced monitoring with Prometheus/Grafana  

---