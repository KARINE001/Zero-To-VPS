# Chapter 4: Connect with Bitvise 🪟

## What is Bitvise?

Free SSH client for Windows. It gives you:
- Terminal (type commands)
- File transfer (drag-and-drop files)
- All-in-one solution

## Step 1: Download Bitvise

1. Go to: `bitvise.com/ssh-client-download`
2. Download "Bitvise SSH Client Installer"
3. Install it (just click Next, Next, Finish)

## Step 2: Open Bitvise

You'll see this window:

```
┌─────────────────────────────────────┐
│    Bitvise SSH Client Login         │
├─────────────────────────────────────┤
│ Server                              │
│   Host:  [ YOUR.IP.HERE ]           │
│   Port:  [ 22 ]                     │
│                                     │
│ Authentication                      │
│   Username:  [ root ]               │
│   Password:  [ ••••••• ]            │
│                                     │
│        [Login] [Cancel]             │
└─────────────────────────────────────┘
```

## Step 3: Enter Your VPS Details

Fill in these fields:

```
┌──────────────────────────────────┐
│ Host:     123.45.67.89           │  ← Your VPS IP
│ Port:     22                     │  ← Leave as 22
│ Username: root                   │  ← Usually "root"
│ Password: YourPassword           │  ← From your VPS email
└──────────────────────────────────┘
```

## Step 4: Click "Login"

First time connecting, you'll see a warning:

```
┌────────────────────────────────────┐
│ The server's host key is unknown  │
│ Do you want to continue?          │
│                                   │
│      [Accept and Save]            │
└────────────────────────────────────┘
```

**Click "Accept and Save"** - this is normal.

## Step 5: Success!

Two windows open:

### 1. Terminal Window
```
┌──────────────────────────────────┐
│ root@yourserver:~#               │
│                                  │
│ This is where you type commands  │
└──────────────────────────────────┘
```

### 2. File Transfer Window
```
┌─────────────────────────────────────┐
│ Your Computer  │   Your VPS          │
│ (left side)    │   (right side)      │
│                │                     │
│ Drag files between these windows!   │
└─────────────────────────────────────┘
```

## Try Your First Command

In the terminal window, type:

```bash
whoami
```

Press Enter. You should see:
```
root
```

**Congratulations!** You broke through the wall! 🎉

## What Just Happened?

```
Your Computer          SSH Connection          Your VPS
┌────────────┐         Encrypted              ┌──────────┐
│  Bitvise   │  ═══════════════════════>      │  Linux   │
│            │   You type: whoami             │          │
│  shows:    │  <═══════════════════════      │ responds:│
│  "root"    │   Result sent back             │  "root"  │
└────────────┘                                └──────────┘
```

## Quick Tips

✅ **Save your session**: Click the profile dropdown, save your connection  
✅ **File transfer**: Drag files between left (your PC) and right (VPS)  
✅ **Multiple sessions**: Can open multiple terminal tabs  
✅ **Keep it open**: Bitvise runs in system tray when you close it  

## Next Steps

Now that you're connected, learn what to type:

👉 **Next:** [Basic Linux Commands](08-basic-linux-commands.md)  
🔙 **Previous:** [First Connection Overview](03-first-connection-overview.md)

---

**You did it!** The invisible wall is gone. You're now controlling your VPS! 🚀
