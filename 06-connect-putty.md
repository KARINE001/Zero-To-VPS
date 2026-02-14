# Chapter 6: Connecting with PuTTY 🖥️

## What is PuTTY?

**PuTTY** is a free, lightweight SSH client for Windows. It's been around since 1999 and is one of the most popular SSH tools.

**Best for:** Simple SSH terminal access, minimal resource usage, and traditional SSH users

**Key Features:**
- Small and fast
- No installation required (portable version available)
- Highly configurable
- Reliable and well-tested

## Step 1: Download PuTTY

### Option A: Installer (Recommended)
1. Go to **putty.org** or **www.chiark.greenend.org.uk/~sgtatham/putty/latest.html**
2. Download **"putty-installer.msi"** (64-bit)
3. Run the installer
4. Click through installation (defaults are fine)

### Option B: Standalone Executable
1. Download **"putty.exe"**
2. Save it anywhere (Desktop, Documents, etc.)
3. Double-click to run - no installation needed!

```
Download PuTTY
      ↓
Install (or just run .exe)
      ↓
Launch PuTTY
```

## Step 2: Get Your VPS Connection Info

```
Required Information:
┌────────────────────────────────┐
│ IP Address:  123.456.789.012   │
│ Port:        22                │
│ Username:    root              │
│ Password:    YourP@ssw0rd      │
└────────────────────────────────┘
```

## Step 3: Configure Your Connection

When you open PuTTY, you'll see the configuration window:

### 3.1 Session Settings

```
┌─────────────────────────────────────┐
│ PuTTY Configuration                 │
├─────────────────────────────────────┤
│ Category:                           │
│  → Session                          │
│                                     │
│ Host Name (or IP address)           │
│ [123.456.789.012]                   │
│                                     │
│ Port                                │
│ [22]                                │
│                                     │
│ Connection type:                    │
│  ○ Raw  ○ Telnet  ● SSH  ○ Serial  │
│                                     │
│ Saved Sessions                      │
│ [My VPS]                            │
│                                     │
│ [Save]  [Load]  [Delete]            │
└─────────────────────────────────────┘
```

**Fill in:**
1. **Host Name:** Your VPS IP address (e.g., `123.456.789.012`)
2. **Port:** `22` (SSH default)
3. **Connection type:** Select **SSH**

### 3.2 Save Your Session (Recommended)

1. In **"Saved Sessions"** field, type a name: `My VPS`
2. Click **"Save"** button
3. Next time, just double-click "My VPS" to load these settings!

```
Why Save?
┌────────────────────────────────┐
│ Without Saving:                │
│ Type IP, Port each time ❌     │
│                                │
│ With Saving:                   │
│ Double-click saved session ✅  │
└────────────────────────────────┘
```

## Step 4: Connect to Your VPS

1. Click **"Open"** button at the bottom
2. A black terminal window opens

### First Connection Warning

You'll see a security alert:

```
┌─────────────────────────────────────────┐
│ PuTTY Security Alert                    │
├─────────────────────────────────────────┤
│ The server's host key is not cached...  │
│                                         │
│ Server's host key fingerprint is:      │
│ ssh-ed25519 256 SHA256:abc123...       │
│                                         │
│ If you trust this host, click "Accept" │
│                                         │
│ [Accept] [Connect Once] [Cancel]       │
└─────────────────────────────────────────┘
```

Click **"Accept"** (or "Yes" in older versions)
- This is normal for first-time connections
- PuTTY saves the fingerprint
- Won't ask again unless something changes

## Step 5: Login

### Enter Username

```
login as: _
```

Type: `root` and press Enter

### Enter Password

```
root@123.456.789.012's password: _
```

Type your password and press Enter
- **Note:** You won't see characters as you type (security feature)
- Just type the password and press Enter

## Step 6: You're Connected! 🎉

You'll see a welcome message:

```
┌──────────────────────────────────────────┐
│ Welcome to Ubuntu 22.04 LTS              │
│                                          │
│ * Documentation: https://help.ubuntu...  │
│                                          │
│ Last login: Fri Feb 14 12:34:56 2024     │
│ root@my-first-vps:~# _                   │
└──────────────────────────────────────────┘
```

You're now at the command prompt! Type commands here.

## Your First Commands

### Check Who You Are
```bash
whoami
```
**Output:** `root`

### See Where You Are
```bash
pwd
```
**Output:** `/root`

### List Files
```bash
ls -la
```
Shows all files in the current directory

### Check System Info
```bash
uname -a
```
Shows Linux kernel and system information

### View System Resources
```bash
top
```
Shows running processes and resource usage  
*Press `q` to quit*

### Update Package Lists
```bash
apt update
```
Checks for available software updates

## Understanding the Terminal

### The Prompt

```
root@my-first-vps:~#
│    │             │ │
│    │             │ └─ # = root user (administrator)
│    │             └─── ~ = home directory (/root)
│    └───────────────── Hostname of your VPS
└────────────────────── Your username
```

### Command Structure

```bash
command  -options  argument
   │         │         │
   │         │         └─ What to act on
   │         └─────────── How to modify behavior
   └───────────────────── What to do
```

**Example:**
```bash
ls -la /var/www
│  │  │
│  │  └─── Look in /var/www directory
│  └────── -l = long format, -a = show hidden files
└───────── List files command
```

## Customizing PuTTY

### Change Font Size

1. Right-click PuTTY window title bar → **"Change Settings"**
2. Go to **Window → Appearance**
3. Click **"Change"** under Font settings
4. Choose larger size (e.g., 12pt or 14pt)
5. Click **"Apply"**

### Change Colors

1. **Change Settings → Colours**
2. Select different color schemes
3. Or customize individual colors

### Popular Color Schemes:
- **Default:** Black background, white text
- **Solarized:** Easy on eyes
- **Monokai:** Dark theme

### Change Window Size

1. **Change Settings → Window**
2. Increase **Columns** (width) and **Rows** (height)
3. Or just resize the window with your mouse!

### Keep Connection Alive

To prevent timeouts:

1. **Change Settings → Connection**
2. Under **"Sending of null packets to keep session active"**
3. Set **"Seconds between keepalives"** to `60`
4. Enable **"Enable TCP keepalives"**
5. Save your session

```
Why This Matters:
Without keepalive → Disconnect after 15 min idle
With keepalive    → Stay connected for hours! ✅
```

## Copying and Pasting

### Copy from PuTTY
- Select text with your mouse
- Text is automatically copied!
- No need to press Ctrl+C

### Paste into PuTTY
- **Right-click** anywhere in the window
- Or **Shift + Insert**
- Or middle mouse button (scroll wheel click)

**Example:**
```bash
# Copy this command from a website:
apt install nginx

# Right-click in PuTTY to paste
# Press Enter to run
```

## Working with Multiple Sessions

### Open Multiple PuTTY Windows

Want to run multiple commands at once?

1. Open PuTTY again (new instance)
2. Load your saved session
3. Click "Open"
4. Login again
5. Now you have two terminals!

```
Window 1                    Window 2
┌──────────────┐           ┌──────────────┐
│ root@vps:~#  │           │ root@vps:~#  │
│ top          │           │ tail -f log  │
│ (monitoring) │           │ (watching)   │
└──────────────┘           └──────────────┘
```

### Different Servers

Save multiple sessions for different VPS:

```
Saved Sessions:
• Production VPS
• Staging VPS  
• Test Server
• Personal VPS
```

## File Transfer with PuTTY (PSCP)

PuTTY includes **PSCP** (PuTTY Secure Copy) for file transfers via command line.

### Upload a File to VPS

**On Windows (Command Prompt):**
```cmd
pscp C:\path\to\file.txt root@123.456.789.012:/root/
```

### Download a File from VPS

```cmd
pscp root@123.456.789.012:/root/file.txt C:\Downloads\
```

**Note:** PSCP is command-line only. For GUI file transfer, use:
- **WinSCP** (free, works great with PuTTY)
- **FileZilla** (free, cross-platform)
- **Bitvise** (has built-in SFTP GUI)

## Using PuTTYgen for SSH Keys

Want password-free login? Generate SSH keys!

### Generate SSH Key Pair

1. Open **PuTTYgen** (installed with PuTTY)
2. Select **"RSA"** or **"Ed25519"**
3. Click **"Generate"**
4. Move mouse randomly to generate randomness
5. **Optional:** Add a passphrase (password for your key)
6. Click **"Save private key"** → Save as `my-vps-key.ppk`
7. Copy the **public key** text (select all in the text box)

### Add Public Key to VPS

1. Connect to VPS with PuTTY (using password)
2. Create .ssh directory:
```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

3. Add your public key:
```bash
nano ~/.ssh/authorized_keys
```
4. Paste your public key (right-click)
5. Press `Ctrl+X`, then `Y`, then Enter to save

6. Set permissions:
```bash
chmod 600 ~/.ssh/authorized_keys
```

### Configure PuTTY to Use Key

1. Open PuTTY configuration
2. Load your saved session
3. Go to **Connection → SSH → Auth**
4. Click **"Browse"** under "Private key file for authentication"
5. Select your `my-vps-key.ppk` file
6. Go back to **Session**, click **"Save"**

Now when you connect, no password needed! 🎉

## Disconnecting Safely

### Option 1: Type exit
```bash
exit
```

### Option 2: Type logout
```bash
logout
```

### Option 3: Close Window
Just click the X - but `exit` is cleaner!

**Remember:** Your VPS keeps running after you disconnect!

## Troubleshooting

### "Network error: Connection refused"
- ❌ Check IP address is correct
- ❌ Check port is 22
- ❌ VPS might be turned off (check provider dashboard)
- ❌ Firewall might be blocking SSH

### "Network error: Connection timed out"
- ❌ Check your internet connection
- ❌ Check IP address is correct
- ❌ VPS might be starting up (wait 2-3 minutes)

### "Access denied"
- ❌ Wrong username (try `root`)
- ❌ Wrong password (case-sensitive!)
- ❌ Caps Lock might be on
- ❌ Check you're typing password correctly (you won't see it)

### "Server refused our key"
- ❌ Public key not added to VPS correctly
- ❌ Permissions on `.ssh` directory or `authorized_keys` file wrong
- ❌ Try password authentication first, then troubleshoot keys

### Connection Keeps Dropping
- ✅ Enable keepalives (see "Customizing PuTTY" section)
- ✅ Check your internet stability
- ✅ Try different network (some routers/firewalls block long SSH sessions)

## PuTTY Tips and Tricks

### 💡 Quick Copy-Paste
Select text = Copy  
Right-click = Paste

### 💡 Full Screen Mode
Press `Alt+Enter` to toggle full screen

### 💡 Scrollback Buffer
Scroll up to see previous output  
Increase buffer: **Window → Lines of scrollback** (default 200, try 2000)

### 💡 Logging Your Session
**Session → Logging** → Save all output to a file for later review

### 💡 Serial Console
PuTTY can also connect to serial ports (useful for some server types)

### 💡 Portable PuTTY
Carry `putty.exe` on a USB drive - works without installation!

## Comparison: PuTTY vs Others

```
┌──────────────┬────────┬──────────┬─────────┐
│              │ PuTTY  │  Bitvise │ VS Code │
├──────────────┼────────┼──────────┼─────────┤
│ Lightweight  │ ⭐⭐⭐⭐⭐ │  ⭐⭐⭐    │   ⭐⭐   │
│ Simple       │ ⭐⭐⭐⭐⭐ │  ⭐⭐⭐⭐   │  ⭐⭐⭐   │
│ File Transfer│   ⭐    │  ⭐⭐⭐⭐⭐  │  ⭐⭐⭐⭐  │
│ For Coding   │   ⭐    │   ⭐⭐    │ ⭐⭐⭐⭐⭐  │
│ Terminal Only│ ⭐⭐⭐⭐⭐ │   ⭐⭐    │   ⭐⭐   │
└──────────────┴────────┴──────────┴─────────┘
```

**Use PuTTY if:** You want a simple, fast SSH terminal  
**Use Bitvise if:** You need file transfers and more features  
**Use VS Code if:** You're developing/coding on your VPS  

## Key Takeaways

✅ PuTTY is lightweight, simple, and reliable  
✅ Perfect for terminal-only SSH access  
✅ Save sessions to avoid retyping connection info  
✅ Enable keepalives to prevent disconnection  
✅ Use PuTTYgen to create SSH keys for password-free login  
✅ Right-click to paste, select to copy  
✅ Use WinSCP with PuTTY for file transfers  

## Up Next

Now that you know how to connect, let's understand what SSH actually is!

👉 **Next:** [Understanding SSH](07-understanding-ssh.md)  
🔙 **Previous:** [Connecting with VS Code](05-connect-vscode.md)

---

**Need definitions?** Check the [Glossary](glossary.md)!
