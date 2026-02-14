# Chapter 4: Connecting with Bitvise SSH Client 🔌

## What is Bitvise?

**Bitvise SSH Client** is a free SSH client for Windows that makes connecting to your VPS super easy. It combines:
- SSH terminal (command line)
- SFTP file transfer (drag-and-drop files)
- Tunneling capabilities

**Best for:** Windows users who want an all-in-one solution

## Step 1: Download and Install Bitvise

1. Go to **bitvise.com/ssh-client-download**
2. Download the installer (free for personal use)
3. Run the installer
4. Click through the installation (defaults are fine)

```
Download
   ↓
Install
   ↓
Launch Bitvise SSH Client
```

## Step 2: Get Your VPS Connection Info

You'll need three things from your VPS provider:

```
Required Information:
┌────────────────────────────────┐
│ IP Address:  123.456.789.012   │  ← From your VPS dashboard
│ Username:    root              │  ← Usually "root"
│ Password:    YourP@ssw0rd      │  ← What you set during setup
└────────────────────────────────┘
```

## Step 3: Configure Bitvise

When you open Bitvise, you'll see the login window:

### 3.1 Server Section

```
┌─────────────────────────────────────┐
│ Server                              │
├─────────────────────────────────────┤
│ Host:  [123.456.789.012]            │  ← Your VPS IP address
│ Port:  [22]                         │  ← Keep as 22 (SSH default)
└─────────────────────────────────────┘
```

**Fill in:**
- **Host:** Your VPS IP address (e.g., `123.456.789.012`)
- **Port:** Leave as `22`

### 3.2 Authentication Section

```
┌─────────────────────────────────────┐
│ Authentication                      │
├─────────────────────────────────────┤
│ Username: [root]                    │  ← Type "root"
│ Password: [••••••••]                │  ← Your VPS password
│                                     │
│ Method: [password ▼]                │  ← Keep as "password"
└─────────────────────────────────────┘
```

**Fill in:**
- **Username:** `root` (the superuser account)
- **Password:** Your VPS password
- **Initial method:** Choose "password"

### 3.3 Save Your Profile (Optional but Recommended)

```
Profile: [My VPS ▼]
         [Save profile]  ← Click this
```

This saves your settings so you don't have to type them again!

## Step 4: Connect!

1. Click the big **"Log in"** button
2. First time connecting, you'll see a security warning:

```
┌────────────────────────────────────────┐
│  Server's Host Key is Unknown          │
├────────────────────────────────────────┤
│  The server's host key is not cached.  │
│                                        │
│  Fingerprint (SHA-256):                │
│  a3:b2:c1:d4:e5:f6:...                 │
│                                        │
│  [Accept and Save]  [Cancel]           │
└────────────────────────────────────────┘
```

3. Click **"Accept and Save"**
   - This is normal for first connection
   - The fingerprint is like the server's ID
   - Saving it means you won't see this again

## Step 5: You're Connected! 🎉

Two windows will open:

### Window 1: Terminal Console (Black Screen)

```
┌─────────────────────────────────────────┐
│ root@my-first-vps:~#                    │
│                                         │
│ Welcome to Ubuntu 22.04 LTS             │
│                                         │
│ * Documentation: https://help.ubuntu... │
│                                         │
│ root@my-first-vps:~# _                  │
└─────────────────────────────────────────┘
```

This is your **command line** - where you type Linux commands!

### Window 2: SFTP Window (File Browser)

```
┌──────────────────┬─────────────────┐
│  Your Computer   │   Your VPS      │
├──────────────────┼─────────────────┤
│  📁 Documents    │  📁 /root       │
│  📁 Downloads    │  📁 /home       │
│  📁 Pictures     │  📁 /var        │
│                  │  📁 /etc        │
└──────────────────┴─────────────────┘
```

This lets you **drag and drop files** between your computer and VPS!

## Your First Commands

Try typing these commands in the terminal:

### Check Who You Are
```bash
whoami
```
**Output:** `root`  
**Meaning:** You're logged in as the root user (administrator)

### See Where You Are
```bash
pwd
```
**Output:** `/root`  
**Meaning:** You're in the root user's home directory

### Check the Date and Time
```bash
date
```
**Output:** `Fri Feb 14 20:14:25 UTC 2024`  
**Meaning:** Shows the server's current date and time

### See System Information
```bash
uname -a
```
**Output:** Shows Linux kernel version and system info

### Update Package List
```bash
apt update
```
This checks for available software updates. You'll see a list scrolling by - this is normal!

## Understanding the Prompt

```
root@my-first-vps:~#
│    │             │ │
│    │             │ └─ # means you're root (admin)
│    │             └─── ~ means you're in home directory
│    └───────────────── Your VPS hostname
└────────────────────── Your username
```

## Using the SFTP Window

### Upload a File to Your VPS
1. Find a file on your computer (left side)
2. Drag it to the right side (VPS)
3. Done! The file is now on your server

### Download a File from Your VPS
1. Find a file on your VPS (right side)
2. Drag it to the left side (your computer)
3. Done! The file is now on your computer

```
Drag & Drop Example:
┌──────────────┐        ┌──────────────┐
│ Your PC      │  ────→ │  VPS         │
│ test.txt     │        │  test.txt    │
└──────────────┘        └──────────────┘
    Upload                  Server has it now!
```

## Bitvise Features

### Opening a New Terminal Tab
- Click **"New terminal console"** button
- You can have multiple terminals open at once

### Connecting to Multiple Servers
- Save different profiles for different VPS servers
- Use the profile dropdown to switch between them

### Port Forwarding (Advanced)
- Click **"Services"** tab
- We'll cover this in advanced tutorials

## Disconnecting Safely

### From the Terminal:
```bash
exit
```
Or just close the window.

### From Bitvise:
- Click the **"X"** on the main window
- Or click **"Log out"**

**Your VPS keeps running** even after you disconnect! That's the point - it's always on.

## Troubleshooting

### "Connection timed out"
- ❌ Check your IP address is correct
- ❌ Check you typed port 22
- ❌ Check your internet connection
- ❌ Your VPS might be turned off (check provider dashboard)

### "Access denied"
- ❌ Check your username is correct (`root`)
- ❌ Check your password is correct (case-sensitive!)
- ❌ Make sure you selected "password" as the method

### "Network error: Connection refused"
- ❌ VPS firewall might be blocking SSH
- ❌ Check if VPS is running in provider dashboard
- ❌ Wait a few minutes (VPS might still be starting up)

### Host Key Changed Warning
```
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED
```
This usually means:
- You reinstalled your VPS (normal)
- Your IP address changed (normal)
- **Rare:** Someone is trying to intercept your connection (security issue)

**Solution:** Click "Accept new key" if you know why it changed.

## Tips and Tricks

### 💡 Save Your Password in Bitvise
- You can save the password in the profile
- Convenient, but only do this on your personal computer
- Don't save passwords on shared computers!

### 💡 Resize the Terminal
- Drag the window edges to make it bigger
- Right-click → Font size to change text size

### 💡 Copy and Paste
- **Copy:** Select text in terminal, it's auto-copied
- **Paste:** Right-click in terminal
- Or use: Ctrl+Shift+V

### 💡 Keep Bitvise Open
- Minimize Bitvise instead of closing it
- Quick access when you need to connect again

## Connection Flow Diagram

```
Your Windows PC                  Internet                 Your VPS
┌──────────────┐                                     ┌─────────────┐
│              │                                     │             │
│   Bitvise    │  ───── Encrypted SSH ─────────→   │  SSH Server │
│   Client     │  ←───── Secure Channel ───────     │  (Port 22)  │
│              │                                     │             │
└──────────────┘                                     └─────────────┘
     Opens                                               Accepts
     │                                                       │
     ├── Terminal Window (commands)                         │
     └── SFTP Window (file transfers)                       │
```

## Key Takeaways

✅ Bitvise is free and easy to use on Windows  
✅ You need: IP address, username (root), and password  
✅ Terminal window = type commands  
✅ SFTP window = transfer files with drag-and-drop  
✅ Your VPS stays running after you disconnect  
✅ Save your profile for quick future connections  

## Up Next

Want to use VS Code instead? Let's see how to connect with VS Code Remote SSH!

👉 **Next:** [Connecting with VS Code](05-connect-vscode.md)  
🔙 **Previous:** [Renting Your First VPS](03-renting-vps.md)

---

**Need term definitions?** Check the [Glossary](glossary.md)!
