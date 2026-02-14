# Chapter 7: Understanding SSH 🔐

## What is SSH?

**SSH** stands for **Secure Shell**. It's a way to securely connect to and control a remote computer over the internet.

Think of it like this:

```
Without SSH (Unsafe):
Your Computer → [Password in plain text!] → Server
                Anyone can read this! ❌

With SSH (Safe):
Your Computer → [Encrypted tunnel 🔒] → Server
                No one can read this! ✅
```

## Why SSH Matters

### Before SSH: Telnet (Scary!)

In the old days, people used **Telnet**:
- Everything sent in plain text
- Passwords visible to anyone snooping
- No encryption whatsoever

```
Telnet Session (1990s):
│ login: root
│ password: mypassword123  ← Everyone can see this! 😱
```

### After SSH: Secure! (1995 - Present)

SSH encrypts everything:
- Commands encrypted
- Passwords encrypted
- File transfers encrypted
- Nobody can read your data

## How SSH Works

### The Connection Process

```
Step-by-step Connection:
┌─────────────────────────────────────────────────┐
│                                                 │
│  1. Your Computer                               │
│     "Hello! I want to connect securely"         │
│            │                                    │
│            ↓                                    │
│  2. VPS Server                                  │
│     "Sure! Here's my public key"                │
│            │                                    │
│            ↓                                    │
│  3. Your Computer                               │
│     "Key looks good! Let's create encryption"   │
│            │                                    │
│            ↓                                    │
│  4. Both                                        │
│     "Encrypted tunnel established! 🔒"          │
│            │                                    │
│            ↓                                    │
│  5. You can now login and work securely         │
│                                                 │
└─────────────────────────────────────────────────┘
```

### What Gets Encrypted

✅ Login credentials (username/password)  
✅ All commands you type  
✅ All output you receive  
✅ Files being transferred  
✅ Everything!  

## SSH Port: 22

SSH typically runs on **port 22**. Think of ports like apartment numbers:

```
Your VPS Building:
┌──────────────────────┐
│ Apartment 22   (SSH) │  ← Port 22
│ Apartment 80   (HTTP)│  ← Port 80
│ Apartment 443 (HTTPS)│  ← Port 443
│ Apartment 3306(MySQL)│  ← Port 3306
└──────────────────────┘
```

When you connect to `123.456.789.012:22`, you're saying:
- Go to building `123.456.789.012`
- Knock on door `22` (SSH service)

## Two Ways to Authenticate

### Method 1: Password Authentication (Simpler)

```
You: "I'm root, my password is: XYZ123"
VPS: "Password correct! You're in."
```

**Pros:**
- ✅ Easy to set up
- ✅ Easy to understand
- ✅ Works immediately

**Cons:**
- ❌ Can be brute-forced (hackers try many passwords)
- ❌ Weak passwords are vulnerable
- ❌ Must type password each time

### Method 2: SSH Key Authentication (More Secure)

```
You: "I'm root, here's my cryptographic proof"
VPS: "Proof matches! You're in."
```

**Pros:**
- ✅ Much more secure
- ✅ No password needed
- ✅ Nearly impossible to brute-force
- ✅ Convenient (auto-login)

**Cons:**
- ❌ Slightly more setup required
- ❌ Must keep private key safe

## Understanding SSH Keys

SSH keys work in pairs, like a lock and key:

```
┌────────────────────────────────────────────┐
│         SSH Key Pair                       │
├──────────────────┬─────────────────────────┤
│  Private Key 🔑  │   Public Key 🔓         │
│  (Keep Secret!)  │   (Share Freely)        │
├──────────────────┼─────────────────────────┤
│  On your PC      │   On your VPS           │
│  Never share     │   Can share with anyone │
│  Like password   │   Like a padlock        │
└──────────────────┴─────────────────────────┘
```

### How Key Authentication Works

```
1. You generate a key pair
   Private Key (yours) + Public Key (shareable)

2. You add public key to VPS
   VPS saves it in ~/.ssh/authorized_keys

3. You try to connect
   Your PC: "I have the private key for this public key"
   VPS: "Prove it!"
   Your PC: [Cryptographic proof using private key]
   VPS: "Correct! You're in!"
```

**The beauty:** Even if someone intercepts the conversation, they can't fake the proof without your private key!

## Creating SSH Keys

### On Windows (PowerShell/Command Prompt)

```powershell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### On Mac/Linux (Terminal)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### The Process:

```
Generating SSH key pair...

1. Save location prompt:
   Enter file in which to save the key (/home/user/.ssh/id_ed25519):
   [Press Enter for default]

2. Passphrase prompt:
   Enter passphrase (empty for no passphrase):
   [Press Enter for no passphrase, or type one for extra security]

3. Confirm passphrase:
   Enter same passphrase again:
   [Press Enter or retype passphrase]

4. Done!
   Your identification has been saved in /home/user/.ssh/id_ed25519
   Your public key has been saved in /home/user/.ssh/id_ed25519.pub
```

### What You Get:

Two files are created:

```
~/.ssh/
├── id_ed25519      ← Private key (KEEP SECRET! 🔑)
└── id_ed25519.pub  ← Public key (safe to share 🔓)
```

## Adding Your Public Key to VPS

### Method 1: Using ssh-copy-id (Easiest - Mac/Linux)

```bash
ssh-copy-id root@123.456.789.012
```

Enter your password one last time, and you're done!

### Method 2: Manual (Windows or if Method 1 doesn't work)

**Step 1:** View your public key

**Windows (PowerShell):**
```powershell
cat $env:USERPROFILE\.ssh\id_ed25519.pub
```

**Mac/Linux:**
```bash
cat ~/.ssh/id_ed25519.pub
```

**Step 2:** Copy the entire output (looks like this):
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAbc123...xyz789 your_email@example.com
```

**Step 3:** Connect to VPS with password:
```bash
ssh root@123.456.789.012
```

**Step 4:** Add key to authorized_keys:
```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
nano ~/.ssh/authorized_keys
```

**Step 5:** Paste your public key, save file:
- Paste the key (right-click or Ctrl+Shift+V)
- Press `Ctrl+X`, then `Y`, then Enter

**Step 6:** Set correct permissions:
```bash
chmod 600 ~/.ssh/authorized_keys
```

**Step 7:** Exit and reconnect:
```bash
exit
ssh root@123.456.789.012
```

No password needed! 🎉

## SSH Configuration File

Make life easier with an SSH config file:

### Create/Edit Config

**Windows:**
```
C:\Users\YourName\.ssh\config
```

**Mac/Linux:**
```
~/.ssh/config
```

### Example Configuration

```ssh
# My Personal VPS
Host myvps
    HostName 123.456.789.012
    User root
    Port 22
    IdentityFile ~/.ssh/id_ed25519

# Production Server
Host production
    HostName 234.567.890.123
    User ubuntu
    Port 22
    IdentityFile ~/.ssh/id_ed25519

# Staging Server
Host staging
    HostName 345.678.901.234
    User deploy
    Port 2222
    IdentityFile ~/.ssh/id_ed25519
```

### Now Connect Simply:

Instead of:
```bash
ssh root@123.456.789.012
```

Just type:
```bash
ssh myvps
```

Much easier! 🚀

## SSH Security Best Practices

### 1. Use SSH Keys Instead of Passwords

```
Password:     🔒 Medium Security
SSH Keys:     🔒🔒🔒🔒 High Security
```

### 2. Use Strong Passwords (If Using Passwords)

```
Bad:  password123         ❌
Bad:  12345678            ❌
Bad:  qwerty              ❌
Good: T8$mK9#pL2@nQ4!     ✅
Good: correct-horse-battery-staple ✅ (long is good!)
```

### 3. Disable Password Authentication (After Setting Up Keys)

Edit SSH config on VPS:
```bash
sudo nano /etc/ssh/sshd_config
```

Find and change these lines:
```
PasswordAuthentication no
PubkeyAuthentication yes
```

Restart SSH:
```bash
sudo systemctl restart ssh
```

Now only SSH keys work! Much more secure.

### 4. Change SSH Port (Optional)

Using port 22 means bots will constantly try to break in. Change it:

Edit SSH config:
```bash
sudo nano /etc/ssh/sshd_config
```

Change:
```
Port 22
```
To:
```
Port 2222
```

Restart SSH:
```bash
sudo systemctl restart ssh
```

Now connect with:
```bash
ssh -p 2222 root@123.456.789.012
```

**Note:** Remember to allow the new port in your firewall!

### 5. Don't Use Root for Everything

We'll cover this more in the security chapter, but:
- Create a normal user account
- Only use root when necessary
- Use `sudo` for admin commands

## Common SSH Commands

### Basic Connection
```bash
ssh username@hostname
```

### Specify Port
```bash
ssh -p 2222 username@hostname
```

### Specify Key File
```bash
ssh -i ~/.ssh/my_key username@hostname
```

### Copy Files (SCP)
```bash
# Upload file to VPS
scp file.txt username@hostname:/path/to/destination/

# Download file from VPS
scp username@hostname:/path/to/file.txt ~/Downloads/

# Copy entire directory
scp -r my_folder username@hostname:/path/to/destination/
```

### Run Single Command
```bash
ssh username@hostname 'ls -la'
```

### SSH Tunneling (Port Forwarding)
```bash
# Access remote port 8080 on your local port 8080
ssh -L 8080:localhost:8080 username@hostname
```

## SSH Host Key Fingerprints

### What Are They?

When you first connect, you see:

```
The authenticity of host '123.456.789.012' can't be established.
ED25519 key fingerprint is SHA256:abc123def456...
Are you sure you want to continue connecting (yes/no)?
```

This is the server's "identity card". It ensures you're connecting to the real server, not an imposter.

### When to Worry

**Normal (Safe):**
- First time connecting to a new server
- After you reinstalled the VPS
- After you changed the SSH configuration

**Warning (Investigate!):**
- You've connected before and suddenly see this warning
- Could be man-in-the-middle attack
- Or server was compromised and reinstalled

**What to do:** Check with your VPS provider if unexpected.

## Troubleshooting SSH

### Permission Denied (Publickey)

```bash
Permission denied (publickey).
```

**Causes:**
- Public key not on server
- Wrong private key
- Permissions wrong on ~/.ssh or keys

**Solutions:**
```bash
# Check permissions
ls -la ~/.ssh

# Should be:
# drwx------  .ssh/          (700)
# -rw-------  id_ed25519     (600)
# -rw-r--r--  id_ed25519.pub (644)
# -rw-------  authorized_keys (600)

# Fix permissions:
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
chmod 600 ~/.ssh/authorized_keys
```

### Connection Timeout

```bash
ssh: connect to host 123.456.789.012 port 22: Connection timed out
```

**Causes:**
- Wrong IP address
- VPS is down
- Firewall blocking port 22
- Internet connection issues

**Solutions:**
- Verify IP address
- Check VPS status in provider dashboard
- Check firewall rules
- Try from different network

### Host Key Verification Failed

```bash
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
```

**This is serious!** It means:
1. Server was reinstalled (probably okay)
2. You're connecting to wrong IP (check!)
3. Man-in-the-middle attack (rare but possible!)

**Solution if you know it's safe:**
```bash
ssh-keygen -R 123.456.789.012
```

This removes the old key, then reconnect.

## Key Takeaways

✅ SSH encrypts everything for security  
✅ Port 22 is the default SSH port  
✅ SSH keys are more secure than passwords  
✅ Private key = secret, Public key = shareable  
✅ Use SSH config file for convenience  
✅ Disable password auth after setting up keys  
✅ Check host key fingerprints on first connection  

## Up Next

Now let's learn basic Linux commands to actually use your VPS!

👉 **Next:** [Linux Basics](08-linux-basics.md)  
🔙 **Previous:** [Connecting with PuTTY](06-connect-putty.md)

---

**Confused about terms?** Check the [Glossary](glossary.md)!
