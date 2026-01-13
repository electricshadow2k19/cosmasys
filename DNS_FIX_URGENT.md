# URGENT: DNS Fix for cosmasys.com

## Current Status
- ✅ `www.cosmasys.com` → Correctly points to GitHub Pages
- ❌ `cosmasys.com` (apex) → Still pointing to GoDaddy (76.223.105.230, 13.248.243.5)

## IMMEDIATE ACTION REQUIRED

### Step 1: Go to GoDaddy DNS Management
1. Log in to GoDaddy
2. Go to **My Products** → Find `cosmasys.com` → Click **DNS**

### Step 2: Delete GoDaddy A Records
**DELETE these A records immediately:**
- Any A record with Name `@` pointing to `76.223.105.230`
- Any A record with Name `@` pointing to `13.248.243.5`
- Any A record with Name `@` pointing to "WebsiteBuilder Site"

### Step 3: Add GitHub Pages A Records
**Add exactly 4 NEW A records** with Name `@`:

1. **A Record 1:**
   - Type: `A`
   - Name: `@`
   - Value: `185.199.108.153`
   - TTL: `600` (or 1 Hour)

2. **A Record 2:**
   - Type: `A`
   - Name: `@`
   - Value: `185.199.109.153`
   - TTL: `600`

3. **A Record 3:**
   - Type: `A`
   - Name: `@`
   - Value: `185.199.110.153`
   - TTL: `600`

4. **A Record 4:**
   - Type: `A`
   - Name: `@`
   - Value: `185.199.111.153`
   - TTL: `600`

### Step 4: Verify CNAME for www
Make sure you have:
- Type: `CNAME`
- Name: `www`
- Value: `electricshadow2k19.github.io`
- TTL: `600`

### Step 5: Save and Wait
1. Click **"Save All Records"**
2. Wait 15-60 minutes for DNS propagation
3. Clear your browser cache
4. Try accessing `cosmasys.com` in incognito mode

## Verification Commands

After making changes, wait 15 minutes, then run:

```powershell
nslookup cosmasys.com
```

**Expected result:** Should show 4 IPs starting with `185.199.108`, `185.199.109`, `185.199.110`, `185.199.111`

**NOT:** `76.223.105.230` or `13.248.243.5` (these are GoDaddy IPs - WRONG!)

## Why This Happens

GoDaddy's website builder creates A records that point to their servers. These need to be **completely removed** and replaced with GitHub Pages IPs.

## After DNS Propagates

1. Go to GitHub: https://github.com/electricshadow2k19/cosmasys/settings/pages
2. Under "Custom domain", enter: `cosmasys.com`
3. Click "Save"
4. Wait a few hours for GitHub to provision SSL certificate
5. Enable "Enforce HTTPS"

## Quick Test

Try accessing:
- `https://www.cosmasys.com` (should work now)
- `https://cosmasys.com` (will work after A records are fixed)

## Still Not Working?

1. **Check DNS propagation:** https://www.whatsmydns.net/#A/cosmasys.com
2. **Clear DNS cache:**
   ```powershell
   ipconfig /flushdns
   ```
3. **Wait longer:** DNS can take up to 48 hours globally
4. **Check GitHub Pages:** Make sure Pages is enabled in repository settings
