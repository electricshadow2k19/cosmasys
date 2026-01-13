# GitHub Pages Deployment with Custom Domain

## Step 1: Enable GitHub Pages

1. Go to your repository: https://github.com/electricshadow2k19/cosmasys
2. Click on **Settings** (top menu)
3. Scroll down to **Pages** in the left sidebar
4. Under **Source**, select:
   - Branch: `main`
   - Folder: `/ (root)`
5. Click **Save**
6. Your site will be available at: `https://electricshadow2k19.github.io/cosmasys/`

## Step 2: Configure Custom Domain on GitHub

1. Still in **Settings → Pages**
2. Under **Custom domain**, enter: `cosmasys.com`
3. Check the box **"Enforce HTTPS"** (this will be available after DNS is configured)
4. Click **Save**

GitHub will automatically create/update the CNAME file in your repository.

## Step 3: Configure DNS on GoDaddy

### Option A: Using A Records (Recommended for apex domain)

1. Log in to your GoDaddy account
2. Go to **My Products** → **DNS** (or **Domain Manager**)
3. Find `cosmasys.com` and click **DNS** or **Manage DNS**
4. You need to add/update these records:

   **A Records** (for apex domain - cosmasys.com):
   - Type: `A`
   - Name: `@` (or leave blank)
   - Value: `185.199.108.153`
   - TTL: 600 (or default)
   
   - Type: `A`
   - Name: `@` (or leave blank)
   - Value: `185.199.109.153`
   - TTL: 600
   
   - Type: `A`
   - Name: `@` (or leave blank)
   - Value: `185.199.110.153`
   - TTL: 600
   
   - Type: `A`
   - Name: `@` (or leave blank)
   - Value: `185.199.111.153`
   - TTL: 600

   **CNAME Record** (for www subdomain):
   - Type: `CNAME`
   - Name: `www`
   - Value: `electricshadow2k19.github.io`
   - TTL: 600

### Option B: Using CNAME (Alternative - requires ALIAS/ANAME if GoDaddy supports it)

If GoDaddy supports ALIAS/ANAME records for the apex domain:
- Type: `ALIAS` or `ANAME`
- Name: `@`
- Value: `electricshadow2k19.github.io`

**Note:** Most registrars don't support CNAME for apex domains, so Option A (A Records) is recommended.

## Step 4: Wait for DNS Propagation

- DNS changes can take **15 minutes to 48 hours** to propagate
- You can check propagation status at: https://www.whatsmydns.net/#A/cosmasys.com
- Once propagated, GitHub will detect the domain and enable HTTPS

## Step 5: Verify HTTPS

1. After DNS propagates (usually within an hour), go back to **Settings → Pages**
2. The **"Enforce HTTPS"** checkbox should become available
3. Check it to enable SSL/HTTPS for your custom domain

## Step 6: Test Your Site

Visit:
- `https://cosmasys.com` (should work)
- `https://www.cosmasys.com` (should redirect to cosmasys.com if configured)

## Troubleshooting

### If the site doesn't load:
1. Check DNS propagation: https://www.whatsmydns.net/#A/cosmasys.com
2. Verify A records are correct in GoDaddy
3. Wait up to 48 hours for full propagation
4. Clear your browser cache

### If HTTPS doesn't work:
1. Make sure DNS is fully propagated
2. Wait a few hours after DNS setup for GitHub to provision SSL certificate
3. Check that "Enforce HTTPS" is enabled in GitHub Pages settings

### Current GitHub Pages IPs (as of 2024):
If the A record IPs change, GitHub updates them here:
https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain

## Important Notes

- The CNAME file in the repository should contain: `cosmasys.com`
- Don't delete the CNAME file - GitHub needs it for custom domain configuration
- If you want www.cosmasys.com to work, configure the CNAME record as shown above
- GitHub Pages is free for public repositories
- Custom domains are free on GitHub Pages
