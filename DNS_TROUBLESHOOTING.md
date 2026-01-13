# DNS Troubleshooting for cosmasys.com

## Current Issues
1. GitHub Pages shows "ADNS check unsuccessful"
2. www.cosmasys.com still shows GoDaddy website builder
3. Domain not resolving to GitHub Pages server

## Steps to Fix

### 1. Verify DNS Records in GoDaddy

Make sure you have EXACTLY these records:

**A Records (for cosmasys.com - apex domain):**
- Name: `@` | Value: `185.199.108.153` | TTL: 600
- Name: `@` | Value: `185.199.109.153` | TTL: 600
- Name: `@` | Value: `185.199.110.153` | TTL: 600
- Name: `@` | Value: `185.199.111.153` | TTL: 600

**CNAME Record (for www.cosmasys.com):**
- Name: `www` | Value: `electricshadow2k19.github.io` | TTL: 600
- **IMPORTANT:** Make sure there's NO trailing dot in the value
- **IMPORTANT:** Make sure there's NO other CNAME or A record for `www`

### 2. Delete ALL Conflicting Records

**Delete these if they exist:**
- Any A record for `@` pointing to "WebsiteBuilder Site" or any GoDaddy IP
- Any CNAME for `www` pointing to `cosmasys.com` or anything other than `electricshadow2k19.github.io`
- Any other records that might conflict

### 3. Check DNS Propagation

After saving changes in GoDaddy, wait 15-30 minutes, then check:

**For apex domain (cosmasys.com):**
- Visit: https://www.whatsmydns.net/#A/cosmasys.com
- Should show: 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153

**For www subdomain:**
- Visit: https://www.whatsmydns.net/#CNAME/www.cosmasys.com
- Should show: electricshadow2k19.github.io

### 4. Clear Browser Cache

After DNS propagates:
- Clear your browser cache
- Try incognito/private browsing mode
- Or use a different browser/device

### 5. Verify in GitHub Pages

Once DNS propagates:
1. Go to GitHub Pages settings
2. Click "Check again" button
3. The error should disappear
4. "Enforce HTTPS" checkbox should become available
5. Enable HTTPS

## Common Issues

### Issue: www still shows GoDaddy site
**Cause:** DNS hasn't propagated yet, or there's a conflicting record
**Solution:** 
- Wait 30-60 minutes after DNS changes
- Verify CNAME record is correct (no trailing dot, correct value)
- Clear browser cache

### Issue: GitHub Pages shows DNS error
**Cause:** DNS records not pointing to GitHub Pages IPs
**Solution:**
- Verify all 4 A records are present and correct
- Make sure no conflicting A records exist
- Wait for DNS propagation (can take up to 48 hours)

### Issue: HTTPS not available
**Cause:** DNS not fully configured or not propagated
**Solution:**
- Wait for DNS to fully propagate
- Make sure GitHub Pages DNS check passes
- Then HTTPS will become available

## Testing Commands

You can test DNS from command line:

**Windows (PowerShell):**
```powershell
# Check A records for apex domain
nslookup cosmasys.com

# Check CNAME for www
nslookup www.cosmasys.com
```

**Expected Results:**
- `cosmasys.com` should resolve to one of the GitHub Pages IPs
- `www.cosmasys.com` should resolve to `electricshadow2k19.github.io`
