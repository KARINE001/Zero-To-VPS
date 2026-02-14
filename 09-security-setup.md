# Chapter 9: Security Setup 🔒

## Why Security Matters

Your VPS is exposed to the entire internet. Within minutes of going online, bots will start trying to break in. This isn't paranoia - it's reality!

```
Your New VPS Goes Online
         ↓
  Within 5 minutes...
         ↓
┌──────────────────────────┐
│ 🤖 Bot: Try password123  │
│ 🤖 Bot: Try admin:admin  │
│ 🤖 Bot: Try root:root    │
│ 🤖 Scanning for exploits │
└──────────────────────────┘
```

**Good news:** Following this chapter makes your VPS 99% more secure!

## Security Checklist

We'll cover:
- ✅ System updates
- ✅ Creating a non-root user
- ✅ SSH key authentication
- ✅ Disabling root login
- ✅ Firewall setup (UFW)
- ✅ Fail2Ban (block attackers)
- ✅ Automatic security updates

## Step 1: Update Your System

**Always do this first!**

```bash
# Update package list
sudo apt update

# Upgrade all packages
sudo apt upgrade -y

# Remove unused packages
sudo apt autoremove -y
```

**Why?**
- Fixes security vulnerabilities
- Patches bugs
- Keeps software current

**How often?** Weekly at minimum, or before any major changes.

## Step 2: Create a Non-Root User

**Never use root for daily tasks!** Create a regular user:

### Create User

```bash
# Create user (replace 'john' with your username)
adduser john
```

You'll be prompted:
```
Enter new UNIX password: ********
Retype new UNIX password: ********
Full Name []: John Smith
Room Number []: [Press Enter]
Work Phone []: [Press Enter]
Home Phone []: [Press Enter]
Other []: [Press Enter]
Is the information correct? [Y/n] Y
```

### Give User Sudo Rights

```bash
# Add user to sudo group
usermod -aG sudo john
```

Now `john` can run admin commands with `sudo`.

### Test New User

```bash
# Switch to new user
su - john

# Test sudo access
sudo apt update

# You'll be asked for YOUR password (not root's)
```

### From Now On: Use Your New User

When connecting via SSH:
```bash
# Instead of:
ssh root@123.456.789.012

# Use:
ssh john@123.456.789.012
```

## Step 3: Set Up SSH Keys

We covered this in Chapter 7, but here's a quick reminder:

### On Your Computer (Generate Key)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### Add Key to Your New User

```bash
# On your computer (Mac/Linux)
ssh-copy-id john@123.456.789.012

# On Windows (PowerShell)
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh john@123.456.789.012 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

### Test Key Authentication

```bash
# Disconnect and reconnect
exit
ssh john@123.456.789.012

# Should connect without password! ✅
```

## Step 4: Harden SSH Configuration

### Edit SSH Config

```bash
sudo nano /etc/ssh/sshd_config
```

### Important Changes

Find and modify these lines:

```bash
# 1. Disable root login
PermitRootLogin no

# 2. Disable password authentication
PasswordAuthentication no

# 3. Only allow your user to login
AllowUsers john

# 4. Change default port (optional but recommended)
Port 2222

# 5. Disable empty passwords
PermitEmptyPasswords no

# 6. Set login grace time
LoginGraceTime 30

# 7. Maximum authentication attempts
MaxAuthTries 3

# 8. Disable X11 forwarding if not needed
X11Forwarding no
```

**Before/After:**
```
BEFORE (Insecure)          AFTER (Secure)
────────────────────────────────────────────
Port 22                  → Port 2222
PermitRootLogin yes      → PermitRootLogin no
PasswordAuthentication yes → PasswordAuthentication no
```

### Save and Restart SSH

```bash
# Save file (Ctrl+O, Enter, Ctrl+X)

# Test configuration (important!)
sudo sshd -t

# If no errors, restart SSH
sudo systemctl restart ssh
```

### Test Connection

**Important:** Keep your current session open! Open a NEW terminal and test:

```bash
# If you changed port to 2222:
ssh -p 2222 john@123.456.789.012

# Should still work! ✅
```

**If it doesn't work:**
- Go back to your original session
- Check the config file
- Look at logs: `sudo tail /var/log/auth.log`

## Step 5: Set Up Firewall (UFW)

**UFW** = Uncomplicated Firewall (and it really is uncomplicated!)

### Install UFW

```bash
sudo apt install ufw -y
```

### Configure Basic Rules

```bash
# 1. Set default policies
sudo ufw default deny incoming
sudo ufw default allow outgoing

# 2. Allow SSH (use your SSH port!)
sudo ufw allow 2222/tcp

# If you didn't change SSH port from 22:
sudo ufw allow 22/tcp

# 3. Allow HTTP and HTTPS (if running web server)
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

### Enable Firewall

```bash
# Enable UFW
sudo ufw enable

# Check status
sudo ufw status verbose
```

**Output should look like:**
```
Status: active

To                         Action      From
--                         ------      ----
2222/tcp                   ALLOW       Anywhere
80/tcp                     ALLOW       Anywhere
443/tcp                    ALLOW       Anywhere
```

### Common UFW Commands

```bash
# Allow specific port
sudo ufw allow 8080/tcp

# Allow from specific IP
sudo ufw allow from 1.2.3.4

# Deny specific port
sudo ufw deny 3306/tcp

# Delete rule
sudo ufw delete allow 8080/tcp

# Reset firewall
sudo ufw reset

# Disable firewall
sudo ufw disable
```

## Step 6: Install Fail2Ban

**Fail2Ban** automatically blocks IPs that try to break in.

### Install

```bash
sudo apt install fail2ban -y
```

### Configure

```bash
# Copy default config
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

# Edit config
sudo nano /etc/fail2ban/jail.local
```

### Basic Configuration

Find and modify these sections:

```ini
[DEFAULT]
# Ban time (in seconds)
bantime = 3600

# Time window to count failures (in seconds)
findtime = 600

# Max number of failures before ban
maxretry = 3

# Email alerts (optional)
destemail = your-email@example.com
sendername = Fail2Ban
action = %(action_mw)s

[sshd]
enabled = true
port = 2222
# Use your actual SSH port!
```

### Start Fail2Ban

```bash
# Start service
sudo systemctl start fail2ban

# Enable at boot
sudo systemctl enable fail2ban

# Check status
sudo systemctl status fail2ban
```

### Check Bans

```bash
# Show banned IPs
sudo fail2ban-client status sshd

# Unban an IP
sudo fail2ban-client set sshd unbanip 1.2.3.4
```

**How it works:**
```
Attacker tries wrong password 3 times
         ↓
Fail2Ban detects pattern
         ↓
Attacker's IP banned for 1 hour
         ↓
They can't even try to connect!
```

## Step 7: Automatic Security Updates

Keep your system updated automatically!

### Install Unattended Upgrades

```bash
sudo apt install unattended-upgrades -y
```

### Configure

```bash
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

Select **"Yes"** when prompted.

### Verify Configuration

```bash
sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```

Make sure these lines are uncommented:
```
"${distro_id}:${distro_codename}-security";
```

### Test

```bash
sudo unattended-upgrade --dry-run --debug
```

## Step 8: Additional Security Measures

### Install Security Utilities

```bash
# Security auditing
sudo apt install lynis -y

# Intrusion detection
sudo apt install rkhunter -y

# Process monitoring
sudo apt install sysstat -y
```

### Run Security Audit

```bash
# Run Lynis audit
sudo lynis audit system

# This will show security recommendations
```

### Disable Unnecessary Services

```bash
# See all running services
systemctl list-unit-files --type=service --state=enabled

# Disable services you don't need (example)
sudo systemctl disable bluetooth
sudo systemctl stop bluetooth
```

### Set Up Automatic Backups

Use your VPS provider's backup service, or:

```bash
# Install backup tool
sudo apt install duplicity -y

# Or use rsync for simple backups
rsync -avz /important/data/ /backup/location/
```

## Security Best Practices

### 1. Strong Passwords

```
Bad:  password123         ❌
Bad:  qwerty              ❌
Good: Tr0ub4dor&3         ✅
Best: correct-horse-battery-staple ✅
```

**Use a password manager:**
- LastPass
- 1Password
- Bitwarden (free, open-source)

### 2. Regular Updates

```bash
# Set up a weekly schedule
# Either manual or automatic via unattended-upgrades
```

### 3. Monitor Logs

```bash
# Check authentication logs
sudo tail -f /var/log/auth.log

# Check system logs
sudo tail -f /var/log/syslog

# Check Fail2Ban logs
sudo tail -f /var/log/fail2ban.log
```

### 4. Principle of Least Privilege

- Don't run everything as root
- Only open ports you actually need
- Only install software you'll use

### 5. Keep Secrets Secret

```bash
# Never commit passwords to git
# Use environment variables
# Use secrets managers

# Example: Store API key
echo "export API_KEY='your-secret-key'" >> ~/.bashrc
source ~/.bashrc
```

### 6. Regular Backups

```
3-2-1 Backup Rule:
3 copies of data
2 different media
1 off-site backup
```

### 7. Two-Factor Authentication

Consider using **Google Authenticator** for SSH:

```bash
sudo apt install libpam-google-authenticator -y
google-authenticator
```

Follow prompts and configure SSH PAM.

## Monitoring Your VPS

### Check Login Attempts

```bash
# Recent successful logins
last

# Recent failed login attempts
sudo lastb

# Current logged-in users
who

# What they're doing
w
```

### Monitor System Resources

```bash
# CPU, Memory, Disk
htop

# Disk usage
df -h

# Network connections
sudo netstat -tulpn
```

### Check for Suspicious Activity

```bash
# Look for failed SSH attempts
sudo grep "Failed password" /var/log/auth.log

# Look for successful root logins (should be none!)
sudo grep "Accepted password for root" /var/log/auth.log

# Check Fail2Ban actions
sudo grep "Ban" /var/log/fail2ban.log
```

## Security Checklist Summary

```
✅ System fully updated (apt update && apt upgrade)
✅ Non-root user created with sudo access
✅ SSH keys configured
✅ Root login disabled
✅ Password authentication disabled
✅ SSH port changed (optional)
✅ UFW firewall enabled
✅ Fail2Ban installed and running
✅ Automatic security updates enabled
✅ Regular backups configured
✅ Monitoring logs regularly
```

## What If Something Goes Wrong?

### Locked Out of SSH

**If you changed SSH config and can't connect:**

1. Log into your VPS provider's console/web terminal
2. Fix the SSH config:
```bash
sudo nano /etc/ssh/sshd_config
```
3. Restart SSH:
```bash
sudo systemctl restart ssh
```

### Firewall Blocking You

**If UFW locked you out:**

1. Use provider's console/web terminal
2. Disable UFW:
```bash
sudo ufw disable
```
3. Fix rules, then re-enable

### Banned by Fail2Ban

```bash
# Check banned IPs
sudo fail2ban-client status sshd

# Unban yourself
sudo fail2ban-client set sshd unbanip YOUR_IP
```

## Common Security Mistakes

### ❌ Don't Do These:

1. **Using root for everything**
   - Create and use a regular user!

2. **Weak passwords**
   - Use strong, unique passwords

3. **No firewall**
   - Always run UFW or iptables

4. **Never updating**
   - Update at least weekly

5. **Opening all ports**
   - Only open what you need

6. **No backups**
   - Backups save you from disasters

7. **Ignoring logs**
   - Monitor for suspicious activity

8. **Sharing credentials**
   - Each person gets their own account

## Testing Your Security

### Port Scan from External Site

Use online tools:
- **shodan.io** - See what's exposed
- **nmap-online.com** - Port scanner

Should only show ports you intentionally opened!

### Check SSH Configuration

```bash
# Test SSH config syntax
sudo sshd -t

# Show SSH configuration
sudo sshd -T
```

### Security Score

```bash
# Run Lynis for security score
sudo lynis audit system

# Review recommendations at end
```

## Key Takeaways

✅ Security is NOT optional - your VPS will be attacked  
✅ Use SSH keys, not passwords  
✅ Disable root login  
✅ Enable UFW firewall  
✅ Install Fail2Ban to block attackers  
✅ Keep system updated (use unattended-upgrades)  
✅ Monitor logs for suspicious activity  
✅ Regular backups save the day  

## You Did It! 🎉

You now have a **secure VPS** that's protected against common attacks. Your server is orders of magnitude safer than most servers on the internet!

## What's Next?

Now you can:
- Install a web server (Nginx, Apache)
- Set up a database (MySQL, PostgreSQL)
- Deploy applications
- Host websites
- Run services

**The world is your oyster!** 🚀

---

👉 **Check:** [Glossary](glossary.md) for any terms you didn't understand  
🔙 **Previous:** [Linux Basics](08-linux-basics.md)  
🏠 **Home:** [Introduction](intro.md)
