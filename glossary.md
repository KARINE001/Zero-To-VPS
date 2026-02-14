# Glossary 📖

A comprehensive list of terms used throughout the Zero-To-VPS guide.

---

## A

**API (Application Programming Interface)**  
A way for programs to communicate with each other. Think of it as a menu at a restaurant - it tells you what you can order and how.

**APT (Advanced Package Tool)**  
Ubuntu/Debian's package manager. Used to install, update, and remove software.  
Example: `apt install nginx`

**Authorized Keys**  
A file (`~/.ssh/authorized_keys`) that contains public SSH keys allowed to log into an account.

**AWS (Amazon Web Services)**  
Amazon's cloud computing platform. Lightsail is their beginner-friendly VPS service.

---

## B

**Bandwidth**  
The amount of data that can be transferred to/from your VPS. Usually measured per month (e.g., 1TB/month).

**Bash**  
The default command-line shell on most Linux systems. Where you type commands.

**Bitvise**  
A popular free SSH client for Windows with built-in file transfer capabilities.

**Bot**  
An automated program. Many bots constantly scan the internet looking for vulnerable servers to attack.

---

## C

**CLI (Command Line Interface)**  
A text-based way to interact with computers by typing commands. Opposite of GUI.

**Cloud**  
Servers and services hosted in data centers and accessed via the internet. "The cloud" is just someone else's computer!

**CPU Core**  
The processing unit of a computer. More cores = better multitasking. "vCore" = virtual core.

**CentOS**  
A Linux distribution popular in enterprise environments. Based on Red Hat Enterprise Linux.

---

## D

**Daemon**  
A background service that runs automatically. Example: SSH daemon (sshd) handles SSH connections.

**Data Center**  
A building full of servers. VPS providers rent space in data centers to host their servers.

**Debian**  
A Linux distribution known for stability. Ubuntu is based on Debian.

**DigitalOcean**  
A popular VPS provider known for developer-friendly features and documentation.

**Droplet**  
DigitalOcean's name for a VPS instance.

---

## E

**Encryption**  
Converting data into a secret code to prevent unauthorized access. SSH uses encryption to protect your connection.

**Ed25519**  
A modern, secure type of SSH key. Recommended over older RSA keys.

---

## F

**Fail2Ban**  
Security software that automatically blocks IP addresses after too many failed login attempts.

**Fingerprint**  
A unique identifier for an SSH server. Used to verify you're connecting to the correct server.

**Firewall**  
Software that controls what network traffic can reach your server. UFW is a popular Linux firewall.

**FQDN (Fully Qualified Domain Name)**  
A complete domain name like `www.example.com` that specifies the exact location of a server.

---

## G

**GUI (Graphical User Interface)**  
A visual way to interact with computers using windows, icons, and buttons. Opposite of CLI.

**GB (Gigabyte)**  
Unit of storage. 1 GB = 1,000 MB. Common VPS sizes: 25 GB, 50 GB, 100 GB.

---

## H

**Hetzner**  
A German VPS provider known for excellent price-to-performance ratio.

**Host Key**  
The SSH key that identifies your server. Used to prevent man-in-the-middle attacks.

**Hostname**  
The name of your server. Example: `my-vps` or `web-server-01`

**Hypervisor**  
Software that creates and manages virtual machines (VPS instances) on physical servers.

**HTTP (HyperText Transfer Protocol)**  
The protocol used for websites. Port 80.

**HTTPS (HTTP Secure)**  
Encrypted version of HTTP. Port 443.

---

## I

**IP Address (Internet Protocol Address)**  
A unique number that identifies your VPS on the internet. Example: `123.456.789.012`

**IPv4**  
The most common IP address format. Looks like: `192.168.1.1`

**IPv6**  
Newer IP address format. Looks like: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

---

## K

**Kernel**  
The core of the operating system. Linux kernel manages hardware and system resources.

**Key Pair**  
Two related cryptographic keys: a private key (kept secret) and public key (shareable). Used for SSH authentication.

---

## L

**Latency**  
The delay in data transmission. Lower is better. Affected by physical distance to server.

**Linode**  
A VPS provider (now owned by Akamai) known for good performance and customer support.

**Linux**  
An open-source operating system. Most VPS servers run Linux. Popular distributions: Ubuntu, Debian, CentOS.

**Load Balancer**  
Distributes traffic across multiple servers. Not needed for beginner VPS setups.

**LTS (Long Term Support)**  
A version of software with extended support. Ubuntu 22.04 LTS gets 5 years of updates.

---

## M

**Man-in-the-Middle Attack**  
When someone secretly intercepts your connection. SSH host keys protect against this.

---

## N

**Nano**  
A beginner-friendly text editor for Linux terminal.

**NIC (Network Interface Card)**  
Hardware (or virtual hardware) that connects your VPS to the network.

---

## O

**OS (Operating System)**  
Software that manages computer hardware and software. Examples: Windows, macOS, Linux.

---

## P

**Package**  
A bundle of software ready to install. Managed by apt on Ubuntu/Debian.

**Package Manager**  
Software that installs, updates, and removes packages. APT on Ubuntu/Debian, YUM on CentOS.

**Passphrase**  
A password that protects your SSH private key. Optional but adds extra security.

**Permissions**  
Rules that control who can read, write, or execute files. Represented as: `rwxr-xr-x`

**Port**  
A numbered communication endpoint. SSH uses port 22, HTTP uses port 80, HTTPS uses port 443.

**Port Forwarding**  
Redirecting traffic from one port to another. Also called tunneling.

**Private Key**  
The secret part of an SSH key pair. Never share this! Keep it on your computer only.

**Public Key**  
The shareable part of an SSH key pair. Added to servers you want to access.

**PuTTY**  
A popular free SSH client for Windows. Lightweight and simple.

---

## R

**RAM (Random Access Memory)**  
Temporary memory for running programs. More RAM = handle more at once. VPS typically have 1-8 GB.

**Root**  
1. The administrator/superuser account with full system control
2. The top-level directory `/` in Linux file system

**RSA**  
An older type of SSH key. Still widely used but Ed25519 is now recommended.

---

## S

**SCP (Secure Copy Protocol)**  
A way to transfer files over SSH securely.

**Server**  
A computer that provides services to other computers. A VPS is a virtual server.

**SFTP (SSH File Transfer Protocol)**  
A secure way to transfer files over SSH. Built into Bitvise and many SSH clients.

**Shell**  
The command-line interface. Bash is the most common shell on Linux.

**SSH (Secure Shell)**  
A protocol for secure remote access to servers. Encrypts everything.

**SSH Client**  
Software used to connect to servers via SSH. Examples: PuTTY, Bitvise, OpenSSH.

**SSH Key**  
A cryptographic key pair used for secure, password-free authentication.

**SSD (Solid State Drive)**  
Fast storage technology. Much faster than traditional hard drives (HDD).

**Sudo**  
Command prefix meaning "do as superuser". Lets regular users run admin commands.  
Example: `sudo apt update`

---

## T

**TB (Terabyte)**  
Unit of data. 1 TB = 1,000 GB. Often refers to monthly bandwidth allowance.

**Terminal**  
The application where you type command-line commands.

**TTY (Teletypewriter)**  
A terminal session. Your connection is a "virtual TTY".

---

## U

**Ubuntu**  
The most popular Linux distribution for VPS servers. Based on Debian, very beginner-friendly.

**UFW (Uncomplicated Firewall)**  
An easy-to-use firewall for Ubuntu/Debian Linux.

**Unattended Upgrades**  
A tool that automatically installs security updates on Ubuntu/Debian.

**Uptime**  
How long a server has been running without downtime. VPS providers advertise 99.9%+ uptime.

---

## V

**vCPU (Virtual CPU)**  
A virtual processor core allocated to your VPS. More vCPUs = better performance for multitasking.

**Virtual Machine**  
A software-based computer running inside a physical computer. Your VPS is a virtual machine.

**VPS (Virtual Private Server)**  
A virtual server that acts like a dedicated server but shares physical hardware with others.

**VS Code (Visual Studio Code)**  
Microsoft's popular code editor with remote SSH capabilities for developing directly on your VPS.

**Vultr**  
A VPS provider known for competitive pricing and many datacenter locations.

---

## W

**Web Console**  
Browser-based terminal provided by VPS hosts. Used if you're locked out of SSH.

**Web Server**  
Software that serves websites. Examples: Nginx, Apache.

---

## Symbols & Conventions

**`~` (Tilde)**  
Represents your home directory.  
`~/files` = `/home/john/files` or `/root/files`

**`/` (Forward Slash)**  
1. Directory separator in Linux paths: `/var/www/html`
2. The root directory (top level of file system)

**`$` (Dollar Sign)**  
In documentation, indicates a regular user command prompt.  
Example: `$ ls`

**`#` (Hash/Pound)**  
1. In documentation, indicates a root user command prompt: `# command`
2. In config files, indicates a comment: `# This is a comment`

**`.` (Dot/Period)**  
1. Current directory: `cd .`
2. Hidden file prefix: `.bashrc`, `.ssh`

**`..` (Double Dot)**  
Parent directory: `cd ..` (go up one level)

**`*` (Asterisk)**  
Wildcard matching any characters.  
`*.txt` = all files ending in `.txt`

**`|` (Pipe)**  
Sends output of one command to another.  
`ls | grep txt`

**`>` (Greater Than)**  
Redirects output to file (overwrites).  
`echo "hello" > file.txt`

**`>>` (Double Greater Than)**  
Redirects output to file (appends).  
`echo "more" >> file.txt`

---

## Common Command Patterns

**`command --help`**  
Shows help for a command.  
Example: `ls --help`

**`man command`**  
Opens the manual page for a command.  
Example: `man ls`

**`command -v`** or **`command --version`**  
Shows version of command.  
Example: `nginx -v`

**`sudo command`**  
Runs command with admin privileges.  
Example: `sudo apt update`

---

## Network & Security Terms

**Brute Force Attack**  
Trying many password combinations to break in. Fail2Ban prevents this.

**DDoS (Distributed Denial of Service)**  
An attack that floods a server with traffic to make it unavailable.

**End-to-End Encryption**  
Data is encrypted from sender to receiver. SSH provides this.

**Man-in-the-Middle**  
An attack where someone intercepts communication between you and the server.

**Packet**  
A small unit of data transmitted over a network.

**Ping**  
A tool to test if a server is reachable. Measures response time.

**SSL/TLS**  
Security protocols for encrypted web connections (HTTPS).

---

## File System Terms

**Absolute Path**  
Full path from root directory.  
Example: `/var/www/html/index.html`

**Relative Path**  
Path relative to current directory.  
Example: `../documents/file.txt`

**Hidden File**  
File starting with a dot. Example: `.bashrc`  
Use `ls -a` to see hidden files.

**Symbolic Link (Symlink)**  
A file that points to another file. Like a shortcut.

---

## Quick Reference

### Essential Commands
- `pwd` - Print working directory
- `ls` - List files
- `cd` - Change directory
- `cp` - Copy
- `mv` - Move/rename
- `rm` - Remove
- `mkdir` - Make directory
- `chmod` - Change permissions
- `chown` - Change owner
- `sudo` - Run as superuser

### Package Management
- `apt update` - Update package list
- `apt upgrade` - Upgrade packages
- `apt install` - Install package
- `apt remove` - Remove package
- `apt search` - Search packages

### System Info
- `whoami` - Current user
- `hostname` - Server name
- `df -h` - Disk space
- `free -h` - Memory usage
- `top` - Process monitor
- `uname -a` - System info

### Networking
- `ip addr` - Show IP addresses
- `ping` - Test connectivity
- `wget` - Download files
- `curl` - Transfer data

### Security
- `ssh` - Connect to server
- `ufw` - Firewall management
- `fail2ban-client` - Check bans
- `chmod` - Set permissions

---

## Still Confused?

If you encounter a term not in this glossary:

1. **Search online**: "what is [term] in Linux"
2. **Use man pages**: `man command`
3. **Check command help**: `command --help`
4. **Ask in forums**: Reddit r/linuxquestions, Stack Overflow

---

🏠 **Return to:** [Introduction](intro.md)  
📚 **Jump to any chapter** from the intro page!

---

*This glossary covers all terms used in the Zero-To-VPS tutorial. Keep it bookmarked for quick reference!*
