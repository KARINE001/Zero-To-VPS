# Chapter 5: Connecting with VS Code 💻

## What is VS Code Remote SSH?

**Visual Studio Code** (VS Code) is a popular code editor that can connect directly to your VPS. This means:
- Edit files on your VPS as if they were on your computer
- Use VS Code's powerful features (IntelliSense, debugging, extensions)
- Terminal built right in
- No need to upload/download files manually

**Best for:** Developers who want to code directly on their VPS

## Step 1: Install VS Code

1. Go to **code.visualstudio.com**
2. Download for your operating system:
   - Windows
   - macOS
   - Linux
3. Install VS Code (follow the installer)

```
Download VS Code
      ↓
Install
      ↓
Launch VS Code
```

## Step 2: Install Remote-SSH Extension

1. Open VS Code
2. Click the **Extensions** icon (left sidebar, or press `Ctrl+Shift+X`)
3. Search for **"Remote - SSH"**
4. Click **Install** on the extension by Microsoft

```
Extensions Marketplace
┌─────────────────────────────────┐
│ Search: Remote - SSH            │
├─────────────────────────────────┤
│ ★★★★★ Remote - SSH              │
│ by Microsoft                    │
│ [Install]                       │
└─────────────────────────────────┘
```

**Also recommended:** Install "Remote - SSH: Editing Configuration Files" (by Microsoft)

## Step 3: Get Your VPS Connection Info

You'll need:

```
Required Information:
┌────────────────────────────────┐
│ IP Address:  123.456.789.012   │
│ Username:    root              │
│ Password:    YourP@ssw0rd      │
└────────────────────────────────┘
```

## Step 4: Connect to Your VPS

### Method 1: Quick Connect (Easiest)

1. Press `F1` or `Ctrl+Shift+P` to open the command palette
2. Type: **"Remote-SSH: Connect to Host"**
3. Select it from the list
4. Type: `root@123.456.789.012` (replace with your IP)
5. Press Enter

```
Command Palette:
┌─────────────────────────────────┐
│ > Remote-SSH: Connect to Host   │
│                                 │
│ Enter: root@your.ip.address     │
└─────────────────────────────────┘
```

6. Choose **"Linux"** as the platform
7. Enter your password when prompted

```
Password Prompt:
┌─────────────────────────────────┐
│ Enter password for root@...     │
│ [••••••••••]                    │
└─────────────────────────────────┘
```

### Method 2: Save Configuration (Recommended)

This saves your connection for easy reuse.

1. Press `F1` or `Ctrl+Shift+P`
2. Type: **"Remote-SSH: Open SSH Configuration File"**
3. Select the first file (usually `C:\Users\YourName\.ssh\config`)
4. Add this configuration:

```ssh
Host my-vps
    HostName 123.456.789.012
    User root
    Port 22
```

**Explanation:**
- `Host my-vps` = Nickname for your server (can be anything)
- `HostName` = Your VPS IP address
- `User` = Username (usually root)
- `Port` = SSH port (22 is standard)

5. Save the file (`Ctrl+S`)
6. Now to connect: Press `F1` → **"Remote-SSH: Connect to Host"** → Choose **"my-vps"**

## Step 5: First Connection Warning

You'll see a fingerprint verification:

```
┌──────────────────────────────────────┐
│ The fingerprint of the host          │
│ 123.456.789.012 is:                  │
│                                      │
│ SHA256:abc123def456...               │
│                                      │
│ Are you sure you want to continue?  │
│                                      │
│ [Continue]  [Cancel]                 │
└──────────────────────────────────────┘
```

Click **"Continue"** - this is normal for first-time connections.

## Step 6: You're Connected! 🎉

VS Code will:
1. Open a new window
2. Show "Opening Remote..." in the bottom left
3. Install VS Code Server on your VPS (one-time setup)
4. Show "SSH: my-vps" in the bottom left corner when ready

```
VS Code Status Bar:
┌──────────────────────────────────┐
│ [SSH: my-vps] ← You're connected!│
└──────────────────────────────────┘
```

## Step 7: Open a Folder on Your VPS

1. Click **File** → **Open Folder**
2. You'll see your VPS's folders, not your computer's!
3. Common starting points:
   - `/root` - Root user's home directory
   - `/var/www` - Web server files (if you install one)
   - `/home` - User home directories

```
Open Folder on VPS:
┌────────────────────────────┐
│ /root                      │  ← Start here
│ /home                      │
│ /var                       │
│ /etc                       │
└────────────────────────────┘
```

## Using VS Code Remote Features

### Built-in Terminal

1. Press `` Ctrl+` `` (backtick) or go to **Terminal → New Terminal**
2. You now have a terminal directly on your VPS!

```
Terminal in VS Code:
┌─────────────────────────────────┐
│ root@my-first-vps:~# _          │
│                                 │
│ Just like SSH, but in VS Code!  │
└─────────────────────────────────┘
```

### Edit Files Directly

1. Click **Explorer** icon (top left)
2. Browse files on your VPS
3. Click any file to edit it
4. Save with `Ctrl+S` - **changes happen directly on your VPS!**

```
File Explorer:
📁 root
├── 📁 .ssh
├── 📄 .bashrc
├── 📄 .profile
└── 📁 projects
    ├── 📄 app.js
    └── 📄 config.json  ← Click to edit
```

### Install Extensions on Remote

Some extensions work on the remote server:

1. Click Extensions icon
2. You'll see two sections:
   - **Local - Installed** (on your computer)
   - **SSH: my-vps - Installed** (on your VPS)
3. Install extensions in the SSH section for remote use

Popular remote extensions:
- Python
- ESLint
- GitLens
- Docker

## Working with Your VPS in VS Code

### Create a New File

1. Right-click in Explorer → **New File**
2. Name it (e.g., `hello.py`)
3. Edit and save
4. The file is now on your VPS!

### Create a New Folder

1. Right-click in Explorer → **New Folder**
2. Name it (e.g., `my-project`)

### Upload Files from Your Computer

**Method 1: Drag and Drop**
- Drag files from your computer into VS Code Explorer
- They'll be uploaded to your VPS!

**Method 2: Copy/Paste**
- Copy file content on your computer
- Paste into a new file in VS Code
- Save

### Run Commands in Terminal

Try these commands in the integrated terminal:

```bash
# Check where you are
pwd

# List files
ls -la

# Create a test file
echo "Hello from my VPS!" > test.txt

# View the file
cat test.txt

# Update packages
sudo apt update
```

## Staying Connected

### Session Persistence
- Your connection stays open as long as VS Code is running
- If you close VS Code, you disconnect (but VPS keeps running)
- Reopen VS Code and reconnect anytime

### Automatic Reconnection
- If internet drops briefly, VS Code tries to reconnect
- You'll see "Attempting to reconnect..." status

### Working Offline
- Can't edit remote files when disconnected
- Terminal commands won't work
- Reconnect to continue

## Advanced: Using SSH Keys Instead of Password

Save time by using SSH keys (no password needed):

### Generate SSH Key (One-time setup)

**On Windows:**
1. Open PowerShell
2. Run:
```powershell
ssh-keygen -t ed25519 -C "your_email@example.com"
```
3. Press Enter (accept default location)
4. Press Enter twice (no passphrase, or create one)

**On Mac/Linux:**
1. Open Terminal
2. Run the same command above

### Copy Key to VPS

**On Windows (PowerShell):**
```powershell
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh root@123.456.789.012 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

**On Mac/Linux:**
```bash
ssh-copy-id root@123.456.789.012
```

Enter your password one last time. Now you can connect without a password!

### Update VS Code Config

Your SSH config now becomes:

```ssh
Host my-vps
    HostName 123.456.789.012
    User root
    Port 22
    IdentityFile ~/.ssh/id_ed25519
```

## Multiple VPS Connections

You can save multiple servers:

```ssh
Host vps1
    HostName 123.456.789.012
    User root

Host vps2
    HostName 234.567.890.123
    User root

Host staging
    HostName 345.678.901.234
    User ubuntu
```

Then pick from the list when connecting!

## Troubleshooting

### "Could not establish connection to remote"
- ✅ Check VPS IP address is correct
- ✅ Check VPS is running (provider dashboard)
- ✅ Check internet connection
- ✅ Try connecting with regular SSH first (to verify credentials)

### Password Prompt Keeps Appearing
- ✅ Check username is correct
- ✅ Check you're typing password correctly (case-sensitive)
- ✅ Consider using SSH keys instead

### "VS Code Server Failed to Start"
- ✅ Your VPS might be out of disk space
- ✅ Run: `df -h` in terminal to check space
- ✅ Clear space or upgrade VPS

### Can't Install Extensions Remotely
- ✅ Some extensions don't support remote
- ✅ Check extension page for "Remote Support" badge
- ✅ Install local version instead

### Connection is Slow
- ✅ Choose closer datacenter region
- ✅ Check your internet speed
- ✅ Large folders can slow down indexing

## Tips and Tricks

### 💡 Open Terminal Quickly
Press `` Ctrl+` `` (backtick key) to toggle terminal

### 💡 Split Terminal
Click the "+" with split icon to have multiple terminals side-by-side

### 💡 Full Screen Terminal
Click the "^" icon to maximize terminal

### 💡 Search Files
Press `Ctrl+P` to quickly find and open files

### 💡 Search in Files
Press `Ctrl+Shift+F` to search for text across all files

### 💡 Git Integration
VS Code's Git features work on remote repos too!

### 💡 Save Your Workspace
**File → Save Workspace As** to remember your open folders and settings

## Comparison: VS Code vs Other Tools

```
┌──────────────┬──────────┬─────────┬────────────┐
│              │ VS Code  │ Bitvise │   PuTTY    │
├──────────────┼──────────┼─────────┼────────────┤
│ Code Editing │  ⭐⭐⭐⭐⭐ │   ⭐     │     ⭐      │
│ Terminal     │  ⭐⭐⭐⭐⭐ │  ⭐⭐⭐⭐  │   ⭐⭐⭐⭐    │
│ File Transfer│  ⭐⭐⭐⭐  │  ⭐⭐⭐⭐⭐ │     ⭐      │
│ Beginner     │  ⭐⭐⭐⭐  │  ⭐⭐⭐⭐⭐ │   ⭐⭐⭐     │
│ Developer    │  ⭐⭐⭐⭐⭐ │  ⭐⭐⭐   │   ⭐⭐      │
└──────────────┴──────────┴─────────┴────────────┘
```

**Use VS Code if:** You want to code/develop on your VPS  
**Use Bitvise if:** You want easy file transfers and general admin  
**Use PuTTY if:** You only need a simple terminal  

## Key Takeaways

✅ VS Code Remote-SSH turns VS Code into a remote development environment  
✅ Edit files directly on your VPS with full VS Code features  
✅ Built-in terminal means no separate SSH client needed  
✅ Save SSH config for quick connections  
✅ SSH keys make connection password-free  
✅ Perfect for developers working on VPS projects  

## Up Next

Want a simpler terminal-only option? Let's try PuTTY!

👉 **Next:** [Connecting with PuTTY](06-connect-putty.md)  
🔙 **Previous:** [Connecting with Bitvise](04-connect-bitvise.md)

---

**Confused by terms?** Check the [Glossary](glossary.md)!
