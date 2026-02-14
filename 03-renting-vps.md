# Chapter 3: Renting Your First VPS 🛒

## Before You Start

Make sure you have:
- ✅ A valid email address
- ✅ A credit/debit card or PayPal account
- ✅ About 10-15 minutes of time

**Don't worry!** Most providers have easy refunds if you change your mind within the first few days.

## Step-by-Step: DigitalOcean Example

We'll use DigitalOcean as our example because it's beginner-friendly. The process is similar for other providers.

### Step 1: Create an Account

1. Go to **digitalocean.com**
2. Click **"Sign Up"** in the top right
3. You can sign up with:
   - Email and password
   - Google account
   - GitHub account

```
┌─────────────────────────────┐
│   DigitalOcean Sign Up      │
├─────────────────────────────┤
│                             │
│  [  Email Address  ]        │
│  [  Password       ]        │
│                             │
│  [ Continue with Google ]   │
│  [ Continue with GitHub ]   │
│                             │
└─────────────────────────────┘
```

**Tip:** Using Google or GitHub is faster and you won't forget your password!

### Step 2: Verify Your Email

1. Check your email inbox
2. Click the verification link
3. This proves you're a real person

### Step 3: Add Payment Method

1. You'll be asked to add a payment method
2. Options usually include:
   - Credit/Debit Card
   - PayPal

```
Payment Options:
┌──────────────┐  ┌──────────────┐
│ Credit Card  │  │   PayPal     │
│              │  │              │
│ [Card Number]│  │ [ Pay with  ]│
│ [Exp Date   ]│  │ [  PayPal   ]│
│ [CVV        ]│  │              │
└──────────────┘  └──────────────┘
```

**Important:** You might see a small charge ($1-5) that's immediately refunded. This is just to verify your card.

### Step 4: Create Your First "Droplet" (VPS)

DigitalOcean calls their VPS servers "Droplets". Let's create one!

#### 4.1 Click "Create" → "Droplets"

```
Dashboard
┌────────────────────────────┐
│  [ Create ▼ ]              │
│     │                      │
│     ├─ Droplets ←── Click  │
│     ├─ Kubernetes          │
│     └─ Databases           │
└────────────────────────────┘
```

#### 4.2 Choose an Operating System

**Recommended for Beginners: Ubuntu 22.04 LTS**

```
Choose an Image:
┌──────────┬──────────┬──────────┬──────────┐
│  Ubuntu  │  Debian  │ CentOS   │  Fedora  │
│   ⭐     │          │          │          │
│  22.04   │   11     │   9      │   37     │
│   LTS    │          │          │          │
└──────────┴──────────┴──────────┴──────────┘
         ▲
    Click this one!
```

**Why Ubuntu?**
- Most popular Linux distribution
- Tons of tutorials and help available
- LTS = Long Term Support (5 years of updates)
- Beginner-friendly

#### 4.3 Choose a Plan

**Start with the Basic/Regular plan:**

```
Plan Options:
┌────────────────────────────────────────┐
│           BASIC / REGULAR              │
├──────────┬──────────┬─────────────────┤
│  $4/mo   │  $6/mo   │  $12/mo         │
├──────────┼──────────┼─────────────────┤
│ 512 MB   │  1 GB    │  2 GB           │
│ 1 vCPU   │  1 vCPU  │  2 vCPU         │
│ 10 GB    │  25 GB   │  50 GB          │
│ 500 GB   │  1 TB    │  2 TB           │
│ Transfer │ Transfer │ Transfer        │
└──────────┴──────────┴─────────────────┘
              ▲
         Recommended!
         Best value for beginners
```

**Our recommendation:** The $6/month plan (1GB RAM, 1 CPU, 25GB storage)

#### 4.4 Choose a Datacenter Region

Pick the one closest to you or your users:

```
Available Regions:
┌─────────────────────────────────┐
│  🇺🇸 New York        NYC1, NYC3  │
│  🇺🇸 San Francisco   SFO3        │
│  🇨🇦 Toronto         TOR1        │
│  🇬🇧 London          LON1        │
│  🇩🇪 Frankfurt       FRA1        │
│  🇳🇱 Amsterdam       AMS3        │
│  🇸🇬 Singapore       SGP1        │
│  🇮🇳 Bangalore       BLR1        │
└─────────────────────────────────┘
```

**Tip:** Hover over regions to see their ping time from your location!

#### 4.5 Authentication Method

You'll see two options:

```
Authentication:
┌─────────────────────────────────┐
│  ○ SSH Key (Recommended)        │
│                                 │
│  ● Password (Easier for now)    │
│    [ Enter password ]           │
└─────────────────────────────────┘
```

**For beginners, choose Password for now.**

We'll learn about SSH keys later (they're more secure), but password is simpler to start.

**Create a strong password:**
- At least 12 characters
- Mix of uppercase, lowercase, numbers, symbols
- Example: `MyVps!2024#Secure`

**💡 Important:** Save this password in a safe place (password manager or notebook)!

#### 4.6 Choose a Hostname

Give your VPS a memorable name:

```
Hostname:
┌─────────────────────────────────┐
│  [my-first-vps]                 │
│                                 │
│  Examples:                      │
│  • my-web-server                │
│  • ubuntu-test                  │
│  • learning-vps                 │
└─────────────────────────────────┘
```

#### 4.7 Additional Options (Skip for Now)

You'll see options like:
- Backups (adds cost)
- Monitoring (can enable later)
- IPv6 (not needed yet)

**For your first VPS, you can skip all these.**

### Step 5: Create the Droplet!

1. Review your choices:
   ```
   Summary:
   • Ubuntu 22.04 LTS
   • $6/month
   • 1GB RAM / 1 vCPU / 25GB SSD
   • New York datacenter
   • Password authentication
   ```

2. Click the big **"Create Droplet"** button

3. Wait 30-60 seconds while it's created

```
Creating your Droplet...
[████████████░░░░░░░░] 60%

This usually takes less than a minute!
```

### Step 6: Your VPS is Ready! 🎉

You'll see your new VPS in the dashboard:

```
Your Droplets:
┌──────────────────────────────────────────┐
│  my-first-vps                   Active   │
├──────────────────────────────────────────┤
│  Ubuntu 22.04 LTS                        │
│  IP Address: 123.456.789.012             │
│  Region: New York                        │
│  1 GB / 1 vCPU / 25 GB                   │
└──────────────────────────────────────────┘
```

**Important Information to Save:**

1. **IP Address** - This is how you'll connect (e.g., `123.456.789.012`)
2. **Username** - Usually `root` for new servers
3. **Password** - The one you created in Step 4.5

## What You Should Have Now

✅ A DigitalOcean account  
✅ A running VPS (Droplet)  
✅ An IP address  
✅ Root username and password  
✅ Email confirmation with details  

## Quick Start with Other Providers

### Vultr
1. Go to vultr.com → Sign Up
2. Click "Deploy New Server"
3. Choose "Cloud Compute"
4. Select Ubuntu 22.04
5. Choose server size ($6/month recommended)
6. Select location
7. Add password
8. Deploy!

### Linode
1. Go to linode.com → Sign Up
2. Click "Create Linode"
3. Choose "Ubuntu 22.04 LTS"
4. Select "Shared CPU" → Nanode 1GB
5. Choose region
6. Create root password
7. Click "Create Linode"

The process is very similar across providers!

## Costs to Expect

```
Monthly Breakdown:
┌────────────────────────────┐
│ VPS Basic Plan:      $6.00 │
│ Bandwidth:          FREE   │ (included)
│ Backups (optional): +$1.20 │ (20% of VPS cost)
├────────────────────────────┤
│ Total:              $6.00  │
└────────────────────────────┘
```

**Billing Notes:**
- Most providers bill hourly (about $0.009/hour)
- If you delete your VPS after 10 days, you only pay for those 10 days
- Monthly maximum is capped (e.g., $6/month)

## Safety Tips

🔒 **Never share your root password**  
💾 **Save your credentials somewhere safe**  
📧 **Keep your account email secure**  
🔍 **Review your bill monthly**  
⚠️ **Set up billing alerts** (most providers offer this)  

## Troubleshooting

### "Payment Failed"
- Check your card details are correct
- Ensure your card supports international transactions
- Try PayPal instead
- Contact your bank (they might have blocked it as "suspicious")

### "Can't Verify Email"
- Check spam/junk folder
- Wait a few minutes (emails can be delayed)
- Use "Resend verification" button

### "Out of Stock in Region"
- Choose a different datacenter location
- Wait a few hours and try again
- Contact support

## Key Takeaways

✅ Creating a VPS takes less than 15 minutes  
✅ Start with Ubuntu 22.04 LTS (most beginner-friendly)  
✅ $5-6/month is perfect for learning  
✅ Save your IP address, username, and password  
✅ You can delete and get refunded if you change your mind  

## Up Next

Now you have a VPS running! Let's connect to it using Bitvise SSH Client.

👉 **Next:** [Connecting with Bitvise](04-connect-bitvise.md)  
🔙 **Previous:** [Choosing a VPS Provider](02-choosing-vps.md)

---

**Confused by any terms?** See the [Glossary](glossary.md)!
