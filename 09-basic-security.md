# Chapter 9: Basic Security 🔒

## Why Security Matters

Your VPS is on the public internet. Bots scan for weak servers 24/7. Basic security is NOT optional.

```
Without Security          With Security
┌──────────────┐         ┌──────────────┐
│ Your VPS     │         │ Your VPS     │
│ Wide Open    │         │ Protected    │
│ ⚠️ Anyone can │         │ ✅ Only you  │
│    try to    │         │    can       │
│    access    │         │    access    │
└──────────────┘         └──────────────┘
```

## The 5 Critical Security Steps

### 1. Update Your System (Do This First!)

```bash
apt update && apt upgrade -y
```

Do this regularly. Updates fix security holes.

### 2. Change Your Root Password

If you're using a default password, change it:

```bash
passwd
```

It will ask for:
1. Current password
2. New password (type it)
3. Confirm new password

**Use a strong password!** Mix letters, numbers, symbols.

### 3. Set Up a Firewall (UFW)

UFW = Uncomplicated Firewall. It blocks unwanted connections.

**⚠️ CRITICAL: Allow SSH port BEFORE enabling the firewall, or you'll lock yourself out!**

```bash
# Install UFW
apt install ufw -y

# Allow SSH FIRST (DON'T SKIP THIS!)
ufw allow 22

# Allow other ports you need (example: web server)
ufw allow 80
ufw allow 443

# Enable firewall
ufw enable

# Check status
ufw status
```

You should see:
```
Status: active

To                         Action
--                         ------
22                         ALLOW
```

### 4. Create a Non-Root User (For Production)

For learning/testing, root is fine. For production nodes, create a regular user:

```bash
# Create new user
adduser yourname

# Give sudo powers
usermod -aG sudo yourname

# Switch to new user
su - yourname
```

Now use this user instead of root. When you need admin power, type `sudo` before commands.

### 5. Install Fail2Ban (Block Attackers)

Fail2Ban blocks IPs that try to brute-force your server.

```bash
# Install
apt install fail2ban -y

# Start it
systemctl start fail2ban
systemctl enable fail2ban

# Check it's running
systemctl status fail2ban
```

That's it! It works automatically.

## Security Checklist

```
✓ Updated system (apt update && apt upgrade)
✓ Changed root password
✓ Enabled firewall (ufw)
✓ Allowed necessary ports (22, 80, 443, etc.)
✓ Installed fail2ban
```

## Node Operator Tip

If your blockchain node needs specific ports, allow them:

```bash
# Example: Allow port 30303 for Ethereum
ufw allow 30303

# Check your node's documentation for required ports!
```

## Quick Visual

```
Before Security           After Security
┌──────────────┐         ┌──────────────────┐
│ All ports    │         │ Only needed      │
│ open         │         │ ports open       │
│              │         │                  │
│ Default      │         │ Strong password  │
│ password     │         │                  │
│              │         │ Fail2Ban blocks  │
│ No protection│         │ attackers        │
└──────────────┘         └──────────────────┘
```

## Key Points

✅ Update system regularly (weekly is good)  
✅ Use strong passwords  
✅ Enable firewall (ufw)  
✅ Only open ports you actually need  
✅ Fail2Ban auto-blocks bad actors  

## What About SSH Keys?

SSH keys are even more secure than passwords. If you want to set them up:

```bash
# On your local computer (not VPS):
ssh-keygen -t ed25519

# Copy to VPS:
ssh-copy-id root@YOUR.VPS.IP

# Then disable password login (optional, advanced):
# Edit: /etc/ssh/sshd_config
# Set: PasswordAuthentication no
# Restart: systemctl restart sshd
```

---

🎉 **Congratulations!** You've completed the Zero-To-VPS guide!

You can now:
- ✅ Connect to your VPS
- ✅ Navigate with Linux commands
- ✅ Keep your server secure
- ✅ Run blockchain nodes or any 24/7 service

**The invisible wall is gone!** 🚀

---

🔙 **Previous:** [Basic Linux Commands](08-basic-linux-commands.md)  
📖 **Reference:** [Glossary](glossary.md)

---

*Keep learning, stay secure, and enjoy your VPS!*
