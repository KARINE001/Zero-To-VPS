# Chapter 6: Connect with PuTTY 🪶

## What is PuTTY?

Lightweight, simple SSH terminal for Windows. Just gives you a terminal window - nothing fancy, but it works great.

## Step 1: Download PuTTY

1. Go to: `www.putty.org`
2. Download "putty.exe" (64-bit)
3. No installation needed - just run it!

## Step 2: Open PuTTY

You'll see this configuration window:

```
┌──────────────────────────────────┐
│        PuTTY Configuration       │
├──────────────────────────────────┤
│ Host Name (or IP address):      │
│ [                             ]  │
│                                  │
│ Port: [22]                       │
│                                  │
│ Connection type:                 │
│  ○ Telnet  ● SSH  ○ Raw         │
│                                  │
│          [Open] [Cancel]         │
└──────────────────────────────────┘
```

## Step 3: Enter Your VPS IP

1. In "Host Name" field: Type your VPS IP address
2. Port: Leave as `22`
3. Connection type: Make sure "SSH" is selected
4. Click "Open"

```
┌──────────────────────────────────┐
│ Host Name: 123.45.67.89          │
│ Port: 22                         │
│ Connection type: ● SSH           │
└──────────────────────────────────┘
```

## Step 4: Security Alert (First Time)

You'll see a warning:
```
┌────────────────────────────────────┐
│ The server's host key is not      │
│ cached in the registry.           │
│                                   │
│ Do you trust this host?           │
│      [Yes] [No] [Cancel]          │
└────────────────────────────────────┘
```

**Click "Yes"** - this is normal for first connection.

## Step 5: Login

A black terminal window opens:

```
┌────────────────────────────────┐
│ login as: █                    │
└────────────────────────────────┘
```

1. Type: `root` and press Enter
2. Type your password (you won't see it as you type - this is normal!)
3. Press Enter

```
login as: root
root@123.45.67.89's password: 
```

## Step 6: Success!

You'll see:

```
┌─────────────────────────────────────┐
│ Welcome to Ubuntu 22.04 LTS         │
│                                     │
│ root@yourserver:~# █                │
└─────────────────────────────────────┘
```

## Try Your First Command

Type:
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
Your Computer      SSH Connection      Your VPS
┌──────────┐      (Encrypted)        ┌──────────┐
│  PuTTY   │   ═════════════════>    │  Linux   │
│ Terminal │    You type: whoami     │  Server  │
│          │   <═════════════════    │          │
│  shows:  │    Result: "root"       │ responds │
│  "root"  │                         │          │
└──────────┘                         └──────────┘
```

## Quick Tips

✅ **Save session**: Before clicking Open, type a name in "Saved Sessions" and click "Save"  
✅ **Copy/Paste**: Right-click to paste, select text to copy  
✅ **Close**: Just X the window when done (or type `exit`)  
✅ **Reconnect**: Open PuTTY, load saved session, click Open  

## Next Steps

Now that you're connected, learn what to type:

👉 **Next:** [Basic Linux Commands](08-basic-linux-commands.md)  
🔙 **Previous:** [First Connection Overview](03-first-connection-overview.md)

---

**You did it!** The invisible wall is gone. You're controlling your VPS! 🚀
