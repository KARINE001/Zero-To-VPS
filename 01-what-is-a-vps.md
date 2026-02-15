# Chapter 1: What is a VPS? 🖥️

## The 5-Second Explanation

**VPS = Virtual Private Server**

It's a computer in a data center that runs 24/7. You rent it, you control it remotely.

## Visual Explanation

```
Your Laptop at Home              Your VPS in Data Center
┌─────────────────┐              ┌──────────────────┐
│  Your Laptop    │              │   Your VPS       │
│  (Sometimes on) │   ─SSH─→     │   (Always on)    │
│  At your desk   │              │   Far away       │
└─────────────────┘              └──────────────────┘
        ↓                                ↓
   You work here                  Your node runs here
   When you want                    24 hours a day
```

## Why Blockchain Node Operators Use VPS

1. **Always online** - Nodes need 24/7 uptime
2. **Fast internet** - Data centers have gigabit speeds
3. **No electricity bills** - Let the data center pay for power
4. **Remote access** - Manage from anywhere
5. **Cheap** - €4-10/month for basic VPS

## What You Get

When you rent a VPS, you get:

```
┌─────────────────────────────┐
│     Your VPS Package        │
├─────────────────────────────┤
│ • Operating System (Linux)  │
│ • CPU cores (1-8+)          │
│ • RAM (1GB-32GB+)           │
│ • Storage (25GB-1TB+)       │
│ • IP address (yours alone)  │
│ • Root access (full control)│
└─────────────────────────────┘
```

## How It Works (Simple)

```
One Big Physical Server in Data Center
┌────────────────────────────────────────┐
│  ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐  │
│  │VPS 1│  │VPS 2│  │VPS 3│  │VPS 4│  │
│  │Your │  │Other│  │Other│  │Other│  │
│  │ One!│  │User │  │User │  │User │  │
│  └─────┘  └─────┘  └─────┘  └─────┘  │
└────────────────────────────────────────┘
```

Each VPS is isolated - others can't see your stuff.

## Key Points

✅ A VPS is a remote computer you rent  
✅ It runs Linux (usually Ubuntu)  
✅ Perfect for blockchain nodes and 24/7 services  
✅ You control it through SSH (we'll learn this)  
✅ Costs about as much as a coffee per week  

---

👉 **Next:** [How to Choose a VPS](02-how-to-choose-a-vps.md)  
🔙 **Previous:** [Introduction](intro.md)
