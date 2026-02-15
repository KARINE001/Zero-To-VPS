# Chapter 7: Understand SSH 🔐

## What is SSH?

**SSH = Secure Shell**

It's the invisible bridge between your computer and your VPS. Everything you type is encrypted before it travels across the internet.

## The Simple Picture

```
Your Computer                 Internet                    Your VPS
┌─────────────┐          ┌──────────────┐           ┌─────────────┐
│             │          │              │           │             │
│ You type:   │  ──────> │  Encrypted   │  ──────>  │  Receives:  │
│ "ls -la"    │          │  Scrambled   │           │  "ls -la"   │
│             │          │  Secure      │           │             │
│ Shows:      │  <────── │  Encrypted   │  <──────  │  Executes   │
│ [files]     │          │  Response    │           │  Command    │
│             │          │              │           │             │
└─────────────┘          └──────────────┘           └─────────────┘
```

No one in the middle can read it!

## Why Port 22?

SSH runs on port 22 by default. Think of it as the VPS's door number for SSH connections.

```
Your VPS has many "doors" (ports):
┌────────────────────────────┐
│ Port 22  → SSH (login)     │  ← We use this one
│ Port 80  → HTTP (websites) │
│ Port 443 → HTTPS (secure)  │
│ Port 3000 → Your app       │
└────────────────────────────┘
```

## Two Ways to Authenticate

### 1. Password (Simple, what you're using now)
```
┌──────────────────────────┐
│ You: root / MyPassword   │
│  ↓                       │
│ VPS: "Password correct,  │
│      welcome!"           │
└──────────────────────────┘
```

Easy but less secure.

### 2. SSH Keys (More Secure, optional)
```
┌─────────────────────────────┐
│ You: Here's my key pair     │
│      (public + private)     │
│  ↓                          │
│ VPS: "Your key matches,     │
│      welcome!"              │
└─────────────────────────────┘
```

Like a physical key instead of a password. Can't be brute-forced.

## What Happens During Connection

```
Step 1: You → "Hey VPS, it's me at 123.45.67.89"
   ↓
Step 2: VPS → "Prove it! Here's my fingerprint"
   ↓
Step 3: You → "Looks good. Here's my password"
   ↓
Step 4: VPS → "Correct! You're in. Here's your shell:"
   ↓
Step 5: root@yourserver:~# █
```

## Key Points

✅ SSH = secure encrypted connection  
✅ Everything you type is scrambled in transit  
✅ Port 22 is the default SSH port  
✅ You can use passwords or SSH keys  
✅ This is why VPS is secure even over public WiFi  

## Optional: SSH Keys (Advanced)

If you want to use SSH keys instead of passwords, they're more secure. Most node operators eventually switch to keys.

**To generate SSH keys:**
```bash
# On your local computer (not VPS):
ssh-keygen -t ed25519

# Then copy to VPS:
ssh-copy-id root@YOUR.VPS.IP
```

After this, you won't need to type password anymore!

---

👉 **Next:** [Basic Linux Commands](08-basic-linux-commands.md)  
🔙 **Previous:** Pick your connection method (Chapters 4-6)

---

**SSH broke the invisible wall. Now let's use that connection!** 🚀
