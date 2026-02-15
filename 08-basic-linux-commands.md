# Chapter 8: Basic Linux Commands 🐧

## Your Terminal Prompt

When you're connected, you see:
```
root@yourserver:~# █
```

This means:
- `root` = your username
- `yourserver` = your VPS hostname
- `~` = you're in home directory
- `#` = you're root user (admin)
- `█` = waiting for your command

## The 6 Essential Commands

### 1. Where Am I? → `pwd`
```bash
pwd
```
Shows your current directory:
```
/root
```

### 2. What's Here? → `ls`
```bash
ls
```
Lists files in current directory.

Better version:
```bash
ls -lah
```
Shows files with details, sizes, hidden files.

### 3. Go Somewhere → `cd`
```bash
cd /var/log        # Go to /var/log
cd ..              # Go up one level
cd ~               # Go to home directory
cd /               # Go to root directory
```

### 4. Read a File → `cat`
```bash
cat filename.txt
```
Shows content of a file.

For long files:
```bash
less filename.txt  # Scroll with arrows, press 'q' to quit
```

### 5. Update System → `apt update && apt upgrade`
```bash
apt update && apt upgrade -y
```
Updates all software on your VPS. Run this regularly!

### 6. Check Running Stuff → `htop`
```bash
htop
```
Shows CPU, RAM usage, running processes. Press 'q' to quit.

If not installed:
```bash
apt install htop -y
```

## Visual File System

```
/                         ← Root (top level)
├── home/                 ← User home folders
├── root/                 ← Your home (as root)
├── var/                  
│   └── log/              ← Log files
├── etc/                  ← Configuration files
└── tmp/                  ← Temporary files
```

## Quick Command Cheat Sheet

```
┌─────────────────────┬──────────────────────────┐
│ Command             │ What It Does             │
├─────────────────────┼──────────────────────────┤
│ pwd                 │ Show current location    │
│ ls                  │ List files               │
│ ls -lah             │ List files (detailed)    │
│ cd /path            │ Change directory         │
│ cat file.txt        │ Show file content        │
│ nano file.txt       │ Edit file                │
│ rm file.txt         │ Delete file              │
│ mkdir newfolder     │ Create folder            │
│ whoami              │ Show current user        │
│ exit                │ Disconnect               │
└─────────────────────┴──────────────────────────┘
```

## Try These Now!

Connect to your VPS and type these:

```bash
# Where am I?
pwd

# What's here?
ls -lah

# What's my username?
whoami

# Update the system
apt update

# See system resources
htop
```

## Key Points

✅ `pwd` = where you are  
✅ `ls` = what's here  
✅ `cd` = go somewhere  
✅ `apt update && apt upgrade` = update system  
✅ Press Tab to autocomplete (try it!)  
✅ Press Up arrow to see previous commands  

## Node Operator Extras

Common commands for blockchain nodes:

```bash
# Check if a service is running
systemctl status your-node-service

# View recent logs
journalctl -u your-node-service -f

# Check disk space
df -h

# Check network connections
netstat -tulpn
```

---

👉 **Next:** [Basic Security](09-basic-security.md)  
🔙 **Previous:** [Understand SSH](07-understand-ssh.md)

---

**You can now navigate and control your VPS!** 🎉
