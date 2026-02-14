# Chapter 8: Linux Basics 🐧

## Welcome to Linux!

Most VPS servers run **Linux**, not Windows or macOS. Don't worry - this chapter teaches you everything you need to know to get started!

Think of Linux like learning to drive a different car - the basics are the same, just some buttons are in different places.

## The Terminal/Command Line

Unlike Windows where you click icons, Linux is mostly controlled by typing commands:

```
┌─────────────────────────────────┐
│ root@my-vps:~# _                │
│                                 │
│ You type commands here          │
│ Press Enter to run them         │
└─────────────────────────────────┘
```

**Why?**
- Faster once you learn it
- More powerful and precise
- Can be automated with scripts
- Uses less resources

## The Linux File System

Everything in Linux is a file or directory (folder). The structure looks like this:

```
/                      ← Root (top level, not root user!)
├── root/              ← Root user's home directory
├── home/              ← Regular users' home directories
│   ├── alice/
│   └── bob/
├── etc/               ← Configuration files
├── var/               ← Variable data (logs, websites)
│   ├── log/          ← Log files
│   └── www/          ← Web server files
├── usr/               ← User programs
├── tmp/               ← Temporary files
└── bin/               ← Essential programs
```

### Important Directories

```
Directory   Purpose                     Example
──────────────────────────────────────────────────
/           Top of everything           /
/root       Root user's home            Your files when logged as root
/home       Users' homes                /home/john
/etc        Configuration files         /etc/ssh/sshd_config
/var/log    Log files                   /var/log/nginx/access.log
/var/www    Web files                   /var/www/html/index.html
/tmp        Temporary files             /tmp/test.txt
/opt        Optional software           /opt/myapp
```

## Basic Navigation Commands

### Where Am I? - `pwd`

**Print Working Directory**

```bash
pwd
```

**Output:** `/root`

This shows your current location in the file system.

### What's Here? - `ls`

**List files and directories**

```bash
# Basic list
ls

# Detailed list
ls -l

# Show hidden files too
ls -a

# Detailed + hidden files
ls -la

# Human-readable sizes
ls -lh
```

**Example Output:**
```
drwxr-xr-x 2 root root 4096 Feb 14 10:00 Documents
-rw-r--r-- 1 root root  156 Feb 14 09:30 notes.txt
-rwxr-xr-x 1 root root 2048 Feb 14 08:00 script.sh
```

**Reading the output:**
```
-rw-r--r--  1  root  root  156  Feb 14 09:30  notes.txt
│           │  │     │     │    │            │
│           │  │     │     │    │            └── File name
│           │  │     │     │    └───────────── Modification date
│           │  │     │     └────────────────── Size (bytes)
│           │  │     └──────────────────────── Group
│           │  └────────────────────────────── Owner
│           └───────────────────────────────── Number of links
└───────────────────────────────────────────── Permissions
```

### Change Directory - `cd`

**Change Directory**

```bash
# Go to a specific directory
cd /var/log

# Go to home directory
cd ~
cd

# Go up one level
cd ..

# Go to previous directory
cd -

# Go down into subdirectory
cd Documents
```

**Example:**
```bash
root@vps:~# cd /var
root@vps:/var# pwd
/var
root@vps:/var# cd log
root@vps:/var/log# pwd
/var/log
root@vps:/var/log# cd
root@vps:~# pwd
/root
```

## File and Directory Commands

### Create Directory - `mkdir`

**Make Directory**

```bash
# Create one directory
mkdir my-project

# Create nested directories
mkdir -p projects/website/css

# Create multiple directories
mkdir docs images scripts
```

### Create Empty File - `touch`

```bash
touch newfile.txt
touch file1.txt file2.txt file3.txt
```

### Copy Files - `cp`

```bash
# Copy file
cp source.txt destination.txt

# Copy directory (recursive)
cp -r my-folder my-folder-backup

# Copy with confirmation
cp -i file.txt file-backup.txt
```

### Move/Rename - `mv`

```bash
# Rename file
mv oldname.txt newname.txt

# Move file to directory
mv file.txt /tmp/

# Move and rename
mv old.txt /var/www/new.txt

# Move multiple files
mv file1.txt file2.txt file3.txt /tmp/
```

### Delete Files - `rm`

**⚠️ Warning: Deletion is permanent! No recycle bin!**

```bash
# Delete file
rm file.txt

# Delete directory (recursive)
rm -r my-folder

# Delete with confirmation
rm -i important.txt

# Force delete (dangerous!)
rm -rf folder
```

**Safety tip:** Always double-check before using `rm -rf`!

### Delete Empty Directory - `rmdir`

```bash
rmdir empty-folder
```

## Viewing File Contents

### View Entire File - `cat`

```bash
cat myfile.txt
```

### View File Page by Page - `less`

```bash
less longfile.txt
```

**Controls:**
- `Space` - Next page
- `b` - Previous page
- `q` - Quit
- `/search` - Search for text

### View First Lines - `head`

```bash
# First 10 lines
head file.txt

# First 20 lines
head -n 20 file.txt
```

### View Last Lines - `tail`

```bash
# Last 10 lines
tail file.txt

# Last 20 lines
tail -n 20 file.txt

# Follow file (watch new lines appear)
tail -f /var/log/syslog
```

**Tip:** `tail -f` is great for watching log files in real-time!

## Editing Files

### Nano (Beginner-Friendly Editor)

```bash
nano filename.txt
```

**Controls:**
- `Ctrl+O` - Save (Write Out)
- `Ctrl+X` - Exit
- `Ctrl+K` - Cut line
- `Ctrl+U` - Paste
- `Ctrl+W` - Search

```
┌─────────────────────────────────┐
│ GNU nano                        │
├─────────────────────────────────┤
│ Hello World!                    │
│                                 │
│ Type your text here             │
│                                 │
├─────────────────────────────────┤
│ ^X Exit  ^O Write Out  ^W Where │
└─────────────────────────────────┘
```

### Quick File Creation with Echo

```bash
# Create file with text
echo "Hello World" > hello.txt

# Append to file
echo "More text" >> hello.txt
```

## Permissions

### Understanding Permissions

```
-rwxr-xr-x
 │││││││││
 ││││││││└─ Execute (others)
 │││││││└── Write (others)
 ││││││└─── Read (others)
 │││││└──── Execute (group)
 ││││└───── Write (group)
 │││└────── Read (group)
 ││└─────── Execute (owner)
 │└──────── Write (owner)
 └───────── Read (owner)
```

**Shorthand:**
- `r` = Read (4)
- `w` = Write (2)
- `x` = Execute (1)

### Change Permissions - `chmod`

```bash
# Make file executable
chmod +x script.sh

# Remove write permission
chmod -w file.txt

# Set specific permissions (755 = rwxr-xr-x)
chmod 755 script.sh

# Set different permissions (644 = rw-r--r--)
chmod 644 document.txt
```

**Common permission numbers:**
```
777 = rwxrwxrwx (everyone can do everything)
755 = rwxr-xr-x (owner full, others read+execute)
644 = rw-r--r-- (owner read+write, others read only)
600 = rw------- (owner only)
```

### Change Owner - `chown`

```bash
# Change owner
sudo chown john file.txt

# Change owner and group
sudo chown john:developers file.txt

# Change recursively
sudo chown -R john:developers /var/www/
```

## System Information

### Current User

```bash
whoami
```

### System Information

```bash
# Operating system info
uname -a

# Distribution info
cat /etc/os-release

# Kernel version
uname -r
```

### Disk Space

```bash
# Disk usage summary
df -h

# Directory size
du -sh /var/www

# Sizes of all directories here
du -h --max-depth=1
```

### Memory Usage

```bash
# Memory info
free -h

# Detailed memory
cat /proc/meminfo
```

### Running Processes

```bash
# All processes
ps aux

# Interactive process viewer
top

# Better process viewer (if installed)
htop
```

**In `top`:**
- `q` - Quit
- `k` - Kill process
- `M` - Sort by memory
- `P` - Sort by CPU

## Package Management (Ubuntu/Debian)

### Update Package Lists

```bash
sudo apt update
```

**Always run this first!** It updates the list of available packages.

### Upgrade Packages

```bash
# Upgrade all packages
sudo apt upgrade

# Upgrade everything (including removing packages if needed)
sudo apt full-upgrade
```

### Install Package

```bash
sudo apt install nginx
sudo apt install mysql-server php
```

### Remove Package

```bash
sudo apt remove nginx
```

### Search for Package

```bash
apt search nginx
```

### Show Package Info

```bash
apt show nginx
```

## Networking Commands

### Check IP Address

```bash
# Show IP addresses
ip addr

# Simpler output
hostname -I
```

### Test Connectivity

```bash
# Ping a server
ping google.com

# Ping 4 times then stop
ping -c 4 google.com
```

### Check Open Ports

```bash
# Show listening ports
sudo netstat -tulpn

# Or with ss (newer)
sudo ss -tulpn
```

### Download Files

```bash
# Download with wget
wget https://example.com/file.zip

# Download with curl
curl -O https://example.com/file.zip
```

## Searching

### Find Files by Name

```bash
# Find in current directory
find . -name "*.txt"

# Find in specific directory
find /var/log -name "*.log"

# Find and delete
find . -name "*.tmp" -delete
```

### Search Inside Files

```bash
# Search for text in file
grep "error" logfile.txt

# Search recursively in directory
grep -r "error" /var/log/

# Case-insensitive search
grep -i "error" file.txt

# Show line numbers
grep -n "error" file.txt
```

## Useful Shortcuts

### Command Line Shortcuts

```
Ctrl+C     Stop current command
Ctrl+D     Exit terminal/logout
Ctrl+L     Clear screen (or type: clear)
Ctrl+A     Go to start of line
Ctrl+E     Go to end of line
Ctrl+U     Delete from cursor to start
Ctrl+K     Delete from cursor to end
Ctrl+R     Search command history
↑ / ↓      Navigate command history
Tab        Auto-complete
```

### Command History

```bash
# Show history
history

# Run previous command
!!

# Run command #123 from history
!123

# Search history
history | grep apt
```

## Pipes and Redirection

### Redirect Output

```bash
# Save output to file (overwrite)
ls > files.txt

# Append output to file
ls >> files.txt

# Redirect errors
command 2> errors.txt

# Redirect output and errors
command > output.txt 2>&1
```

### Pipe Output to Another Command

```bash
# Pipe examples
ls -l | grep ".txt"
cat file.txt | sort
ps aux | grep nginx
cat /var/log/syslog | tail -n 50 | grep error
```

## System Management

### Restart Services

```bash
sudo systemctl restart nginx
sudo systemctl restart ssh
```

### Start/Stop Services

```bash
sudo systemctl start nginx
sudo systemctl stop nginx
```

### Check Service Status

```bash
sudo systemctl status nginx
```

### Enable Service at Boot

```bash
sudo systemctl enable nginx
```

### Reboot System

```bash
sudo reboot
```

### Shutdown System

```bash
sudo shutdown now
sudo shutdown -h +10  # Shutdown in 10 minutes
```

## Quick Reference Cheat Sheet

```
NAVIGATION          FILE OPERATIONS      VIEWING FILES
pwd                 mkdir dir            cat file
ls                  touch file           less file
ls -la              cp src dst           head file
cd dir              mv src dst           tail file
cd ~                rm file              tail -f file
cd ..               rm -r dir            nano file

PERMISSIONS         SYSTEM INFO          SEARCH
chmod 755 file      whoami               find . -name "*.txt"
chmod +x file       df -h                grep "text" file
chown user file     free -h              grep -r "text" dir

PACKAGES            NETWORK              PROCESS
apt update          ip addr              ps aux
apt install pkg     ping host            top
apt remove pkg      wget url             kill PID
```

## Practice Exercises

Try these safe commands on your VPS:

```bash
# 1. Navigate and explore
cd /var
ls -la
cd log
ls
cd ~

# 2. Create a test project
mkdir -p ~/test-project/docs
cd ~/test-project
touch README.md
echo "# My Project" > README.md
cat README.md

# 3. File operations
cp README.md README-backup.md
ls -l
mv README-backup.md backup/README.md
rm backup/README.md

# 4. System info
df -h
free -h
whoami
hostname
```

## Key Takeaways

✅ Linux uses commands instead of clicks  
✅ File system starts at `/` (root)  
✅ `ls`, `cd`, `pwd` for navigation  
✅ `cp`, `mv`, `rm` for file operations (be careful with `rm`!)  
✅ `nano` for editing files  
✅ `apt` for installing software  
✅ Permissions control who can read/write/execute files  
✅ Tab key auto-completes - use it!  

## Up Next

Now let's secure your VPS properly!

👉 **Next:** [Security Setup](09-security-setup.md)  
🔙 **Previous:** [Understanding SSH](07-understanding-ssh.md)

---

**Need definitions?** See the [Glossary](glossary.md)!
