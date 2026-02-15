# Chapter 5: Connect with VS Code 👨‍💻

## What is VS Code Remote?

If you already use VS Code for coding, you can use it to connect to your VPS and edit files remotely.

## Step 1: Install VS Code

If you don't have it:
1. Go to: `code.visualstudio.com`
2. Download and install

## Step 2: Install Remote-SSH Extension

1. Open VS Code
2. Click Extensions icon (left sidebar, or Ctrl+Shift+X)
3. Search: "Remote - SSH"
4. Install the one by Microsoft

```
┌────────────────────────────────┐
│ Extensions                     │
├────────────────────────────────┤
│ Search: Remote - SSH           │
│                                │
│ ✓ Remote - SSH                 │
│   by Microsoft                 │
│   [Install]                    │
└────────────────────────────────┘
```

## Step 3: Connect to Your VPS

1. Press `F1` (or Ctrl+Shift+P)
2. Type: "Remote-SSH: Connect to Host"
3. Click it
4. Select "Add New SSH Host"

```
┌────────────────────────────────┐
│ Enter SSH Connection Command:  │
│                                │
│ ssh root@123.45.67.89          │
└────────────────────────────────┘
```

Type: `ssh root@YOUR.VPS.IP` and press Enter

## Step 4: First Connection

1. VS Code will ask for your password
2. Type your VPS password
3. First time: Click "Continue" when it asks about fingerprint

```
┌────────────────────────────────────┐
│ Enter password for root@123.45... │
│                                    │
│ Password: [••••••••]               │
└────────────────────────────────────┘
```

## Step 5: Success!

Bottom left corner shows:
```
┌────────────────┐
│ SSH: 123.45... │
└────────────────┘
```

You're connected! Now:
- Click "Open Folder" → Choose `/root`
- Open the terminal: View → Terminal (or Ctrl+`)

## Try Your First Command

In the terminal at the bottom, type:

```bash
whoami
```

You should see: `root`

**Congratulations!** 🎉

## What You Can Do Now

```
┌─────────────────────────────────────┐
│         VS Code Window              │
├─────────────────────────────────────┤
│ File Explorer    │  Code Editor     │
│ (left)           │  (center)        │
│                  │                  │
│ • See VPS files  │  • Edit files    │
│ • Navigate dirs  │  • Save directly │
│                  │    to VPS        │
├─────────────────────────────────────┤
│      Terminal (bottom)              │
│      root@yourserver:~#             │
│      (Type commands here)           │
└─────────────────────────────────────┘
```

## Quick Tips

✅ **Save connection**: VS Code remembers it - next time click "Recent"  
✅ **Open terminal**: Ctrl+` (backtick)  
✅ **Edit files**: Click any file in explorer, edit, save → saves to VPS  
✅ **Install extensions**: They run on the VPS, not locally  

## Next Steps

Now that you're connected, learn what to type:

👉 **Next:** [Basic Linux Commands](08-basic-linux-commands.md)  
🔙 **Previous:** [First Connection Overview](03-first-connection-overview.md)

---

**You did it!** You're now controlling your VPS from VS Code! 🚀
