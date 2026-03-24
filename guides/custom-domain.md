# Setting Up a Custom Domain

Use your own domain instead of `docsbook.io` for your documentation.

**Required:** Premium subscription ($29 one-time)

## Why Use a Custom Domain?

### Benefits

- 🎯 **Branding** — documentation under your own domain
- 📈 **SEO** — links to your domain improve your ranking
- 🔐 **Trust** — visitors see your domain, not someone else's
- 💼 **Professionalism** — looks like your own product

### Examples

```
❌ Without domain:
docsbook.io/mycompany/product

✅ With domain:
docs.mycompany.com
```

## Requirements

1. **Your own domain** — registered by you
   - If you don't have one — buy on [GoDaddy](https://www.godaddy.com), [Namecheap](https://www.namecheap.com), or another registrar

2. **Premium subscription** — $29 one-time
   - If you haven't upgraded yet — [do it now](./premium.md)

3. **Access to DNS settings** — at your domain registrar

## Step 1: Open Settings

1. View your documentation while logged in
2. Click the Float Widget in the bottom right
3. Open **Settings**

## Step 2: Enter Your Domain

In the **Custom Domain** section:

1. Enter your domain (e.g., `docs.example.com`)
2. Click **Save**

Docsbook will generate the DNS configuration.

## Step 3: Update DNS

Docsbook will provide instructions:

```
Add a CNAME record:
Type:  CNAME
Name:  docs (or @)
Value: cname.vercel-dns.com
```

### Where to Change DNS?

Open the control panel of your domain registrar:

#### GoDaddy

1. Open [godaddy.com](https://godaddy.com) → Sign in
2. My Domains → Select domain → DNS
3. Click "Add" next to DNS
4. Fill in:
   - Type: CNAME
   - Name: `docs`
   - Points to: `cname.vercel-dns.com`
5. Save

#### Namecheap

1. Open [namecheap.com](https://namecheap.com) → Sign in
2. Domain List → Manage
3. Advanced DNS
4. Add new record:
   - Type: CNAME
   - Host: `docs`
   - Value: `cname.vercel-dns.com`
   - TTL: 3600
5. Save

#### Google Domains

1. Open [domains.google.com](https://domains.google.com)
2. Select domain
3. DNS → Custom records
4. Create new record:
   - DNS Record Type: CNAME
   - Name: `docs`
   - Data: `cname.vercel-dns.com`
5. Save

#### 1and1 / Ionos

1. Sign in → Domains
2. Select domain
3. Manage DNS
4. Add record:
   - Type: CNAME
   - Subdomain: `docs`
   - Alias: `cname.vercel-dns.com`
5. Save

### Using a Root Domain

If you want `example.com` (without `docs`):

1. **Our recommendation:** use `docs.example.com`
   - Easier to configure
   - Lets you use `example.com` for the project site

2. **If you still want root:**
   - Some registrars don't allow CNAME on root
   - Use an A record instead of CNAME: `76.76.19.0`
   - Contact [support@docsbook.io](mailto:support@docsbook.io) for help

## Step 4: Wait

After adding the DNS record, updates propagate:

- **Usually:** 15-30 minutes
- **Maximum:** 48 hours
- **Check status:** use [DNSChecker](https://dnschecker.org)

Enter your domain → it should show `cname.vercel-dns.com`

## Step 5: SSL Certificate

Once DNS propagates, Docsbook automatically:

1. Detects your domain
2. Creates an SSL certificate (Let's Encrypt)
3. Enables HTTPS

Your site is available at:

```
https://docs.example.com ✅
```

## Verifying Your Domain

### How to check everything is working?

**Method 1: Simple check**
1. Open in browser: `https://your-domain.com`
2. Your documentation should load

**Method 2: DNS check**
```bash
# In terminal
nslookup docs.example.com
# Should show: cname.vercel-dns.com
```

**Method 3: Online service**
1. Open [mxtoolbox.com](https://mxtoolbox.com)
2. CNAME lookup
3. Enter your domain
4. Should show `cname.vercel-dns.com`

## Troubleshooting

### DNS Not Updating

**Problem:** 2+ hours have passed, but domain doesn't work

**Solutions:**
1. Clear browser cache (Ctrl+Shift+Delete)
2. Use a private browser window
3. Check DNS via [DNSChecker](https://dnschecker.org)
4. Verify the CNAME record is added correctly
5. Wait another 24 hours

### Old Site Still Showing

**Problem:** DNS updated, but old version of site

**Solutions:**
1. Press Ctrl+F5 (full cache clear)
2. Open in private window
3. Wait 24 hours

### HTTPS Not Working

**Problem:** `https://` shows a certificate error

**Solutions:**
1. Wait 1 hour — certificate is being created
2. Make sure DNS has updated
3. Check domain name for typos
4. Contact [support@docsbook.io](mailto:support@docsbook.io)

### Domain Shows Vercel or Error

**Problem:** Visiting the domain shows a Vercel message

**Solutions:**
1. Check the domain is added in Docsbook (visible in Settings)
2. Make sure the DNS CNAME is correct
3. Wait 1-2 hours for sync

## Changing Your Domain

### How to switch to a different one?

1. Open settings
2. Change the domain in the **Custom Domain** field
3. Click Save
4. Update DNS for the new domain
5. The old domain will stop working

## Removing Your Domain

### How to go back to docsbook.io?

1. Open settings
2. Clear the **Custom Domain** field
3. Click Save

Documentation returns to:
```
docsbook.io/username/repo
```

## Best Practices

### 1. Use a Subdomain

```
✅ docs.example.com
✅ guide.example.com
✅ api.example.com

❌ example.com (if your main site is there)
```

### 2. Tell People About the Domain

Update links to your documentation everywhere:
- GitHub README
- Project website
- Email signatures
- Social media

### 3. Set Up Email (Optional)

Now that you have a domain, you can add email:
- [Google Workspace](https://workspace.google.com) — professional Gmail
- [Zoho Mail](https://www.zoho.com/mail) — free option
- [Protonmail](https://proton.me) — private email

This is a separate service from Docsbook, configured through your registrar.

### 4. Use for SEO

Now that the site is under your domain:
- Set up Google Analytics
- Track traffic
- Submit to search engines

## What's Next?

- [Translating Documentation](./translation.md)
- [More Premium Features](./premium.md)
- [Managing Documentation](./managing-docs.md)
