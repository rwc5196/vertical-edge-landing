# VERTICAL EDGE LANDING PAGE — MASTER DEPLOYMENT GUIDE

**Protocol:** CITADEL v5 + NEXUS v2.3C Validated  
**Status:** READY FOR IMMEDIATE EXECUTION  
**Total Time:** ~35 minutes (20 deploy + 15 verify)  
**Target URL:** https://verticaledgeai.ai  

---

## TABLE OF CONTENTS

1. [Pre-Flight Checklist](#1-pre-flight-checklist)
2. [Phase 1: GitHub Repository Setup](#2-phase-1-github-repository-setup-5-min)
3. [Phase 2: Netlify Deployment](#3-phase-2-netlify-deployment-3-min)
4. [Phase 3: DNS Configuration](#4-phase-3-dns-configuration-5-min)
5. [Phase 4: Favicon Generation](#5-phase-4-favicon-generation-5-min)
6. [Phase 5: Verification](#6-phase-5-verification-15-min)
7. [Phase 6: Post-Deployment Integration](#7-phase-6-post-deployment-integration)
8. [Troubleshooting](#8-troubleshooting)
9. [Reference Links](#9-reference-links)

---

## 1. PRE-FLIGHT CHECKLIST

Before starting, confirm you have:

```
[ ] Landing page files ready (index.html, assets/, etc.)
[ ] GitHub account (github.com)
[ ] Netlify account (netlify.com) — free tier is sufficient
[ ] DNS access for verticaledgeai.ai
[ ] ~35 minutes of uninterrupted time
```

### Required Files Structure

```
vertical-edge-landing/
├── index.html                    # Main landing page (with Netlify Forms configured)
├── assets/
│   └── images/
│       ├── og-image.png          # 1200x630px Open Graph image
│       └── favicon.ico           # Generated in Phase 4
├── README.md                     # Project documentation
└── netlify.toml                  # (Optional) Netlify configuration
```

### Verify Netlify Forms Configuration

Before deploying, confirm your `index.html` form has the correct attributes:

```html
<!-- CORRECT: Netlify Forms configuration -->
<form class="contact-form" name="contact" method="POST" data-netlify="true" netlify-honeypot="bot-field">
    <!-- Honeypot field for spam protection (hidden) -->
    <p class="hidden" style="display:none;">
        <label>Don't fill this out: <input name="bot-field" /></label>
    </p>
    
    <input type="text" name="name" class="form-input" placeholder="Your name" required>
    <input type="email" name="email" class="form-input" placeholder="Work email" required>
    <textarea name="message" class="form-input" placeholder="What's your biggest operational challenge?" required></textarea>
    <button type="submit" class="btn btn-secondary" style="width: 100%;">Send Message</button>
</form>
```

**Critical attributes:**
- `name="contact"` — Form identifier in Netlify dashboard
- `data-netlify="true"` — Enables Netlify Forms processing
- `netlify-honeypot="bot-field"` — Spam protection

---

## 2. PHASE 1: GITHUB REPOSITORY SETUP (5 min)

### Step 1.1: Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: `vertical-edge-landing`
3. Description: `Vertical Edge AI landing page`
4. Visibility: **Private** (recommended for business assets)
5. Do NOT initialize with README (you have local files)
6. Click **Create repository**

### Step 1.2: Initialize Local Repository

Open terminal in your project directory and execute:

```bash
# Navigate to your landing page directory
cd "c:\Users\Ryan\Documents\Claude 4.5\!!! AI Network - MVP !!!\Landing"

# Initialize git repository
git init

# Add all files to staging
git add .

# Create initial commit
git commit -m "Initial commit: Vertical Edge AI landing page"

# Add GitHub remote (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/vertical-edge-landing.git

# Rename branch to main (if needed)
git branch -M main

# Push to GitHub
git push -u origin main
```

### Step 1.3: Verify Push Success

```bash
# Verify remote is set correctly
git remote -v

# Expected output:
# origin  https://github.com/YOUR_USERNAME/vertical-edge-landing.git (fetch)
# origin  https://github.com/YOUR_USERNAME/vertical-edge-landing.git (push)
```

**✓ CHECKPOINT:** Visit your GitHub repo URL — you should see all files.

---

## 3. PHASE 2: NETLIFY DEPLOYMENT (3 min)

### Step 2.1: Connect Repository to Netlify

1. Go to https://app.netlify.com
2. Click **"Add new site"** → **"Import an existing project"**
3. Select **"Deploy with GitHub"**
4. Authorize Netlify to access your GitHub (if first time)
5. Select repository: `vertical-edge-landing`

### Step 2.2: Configure Build Settings

For a static HTML site, use these settings:

```
Branch to deploy: main
Base directory: (leave blank)
Build command: (leave blank)
Publish directory: (leave blank or /)
```

Click **"Deploy site"**

### Step 2.3: Wait for Deployment

- Netlify will assign a random subdomain: `[random-name].netlify.app`
- Deployment typically completes in 30-60 seconds
- Watch the deploy log for any errors

**✓ CHECKPOINT:** Visit `https://[random-name].netlify.app` — your site should be live.

### Step 2.4: Rename Netlify Subdomain (Optional)

1. Go to **Site settings** → **Domain management** → **Domains**
2. Click on the `.netlify.app` domain
3. Click **"Options"** → **"Edit site name"**
4. Change to: `verticaledgeai` 
5. New URL: `https://verticaledgeai.netlify.app`

---

## 4. PHASE 3: DNS CONFIGURATION (5 min)

### Domain Strategy Decision

**RECOMMENDED: Option A — Apex Domain with www Redirect**

| URL | Behavior |
|-----|----------|
| `verticaledgeai.ai` | Primary (serves site) |
| `www.verticaledgeai.ai` | Redirects to apex |

### Step 3.1: Add Custom Domain in Netlify

1. Go to **Site settings** → **Domain management** → **Domains**
2. Click **"Add custom domain"**
3. Enter: `verticaledgeai.ai`
4. Click **"Verify"** → **"Add domain"**
5. Repeat for: `www.verticaledgeai.ai`

### Step 3.2: Configure DNS Records

**CRITICAL:** The Netlify dashboard will show you the exact IP address and DNS records needed. Use those values, not hardcoded IPs from documentation.

Typically, you'll need to add these records in your DNS provider:

```
# Apex domain (verticaledgeai.ai)
Type: A
Name: @ (or leave blank)
Value: [IP shown in Netlify dashboard]
TTL: 3600 (or Auto)

# WWW subdomain
Type: CNAME
Name: www
Value: [your-site].netlify.app
TTL: 3600 (or Auto)
```

**Common Netlify Load Balancer IPs (verify in dashboard):**
- 75.2.60.5
- 99.83.190.102

### Step 3.3: Wait for DNS Propagation

- Can take 5 minutes to 48 hours (usually <30 minutes)
- Netlify will automatically provision SSL certificate once DNS resolves

### Step 3.4: Verify DNS Configuration

```bash
# Check A record
dig verticaledgeai.ai +short

# Check CNAME
dig www.verticaledgeai.ai +short

# Check if site is accessible
curl -I https://verticaledgeai.ai
```

**Expected curl output:**
```
HTTP/2 200
...
```

**✓ CHECKPOINT:** Both `verticaledgeai.ai` and `www.verticaledgeai.ai` load your site.

---

## 5. PHASE 4: FAVICON GENERATION (5 min)

### Step 4.1: Generate Favicon

1. Go to https://favicon.io/favicon-generator/
2. Configure:
   - **Text:** VE
   - **Background:** Circle
   - **Font Family:** Leckerli One (or any bold sans-serif)
   - **Font Size:** 70
   - **Font Color:** #FFFFFF (white)
   - **Background Color:** #4F40E5 (indigo — matches brand)
3. Click **"Download"**
4. Extract the ZIP file

### Step 4.2: Add Favicon Files to Project

Copy these files from the downloaded ZIP to your `assets/images/` folder:
- `favicon.ico`
- `favicon-16x16.png`
- `favicon-32x32.png`
- `apple-touch-icon.png`
- `android-chrome-192x192.png`
- `android-chrome-512x512.png`

### Step 4.3: Update HTML Head

Add these lines to the `<head>` section of `index.html`:

```html
<!-- Favicon -->
<link rel="apple-touch-icon" sizes="180x180" href="assets/images/apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="32x32" href="assets/images/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="assets/images/favicon-16x16.png">
<link rel="icon" type="image/x-icon" href="assets/images/favicon.ico">
```

### Step 4.4: Push Favicon Update

```bash
git add .
git commit -m "Add favicon files"
git push
```

Netlify will auto-deploy the update within ~60 seconds.

**✓ CHECKPOINT:** Refresh your site — favicon should appear in browser tab.

---

## 6. PHASE 5: VERIFICATION (15 min)

### Step 5.1: Form Submission Test

**Browser Test:**
1. Go to https://verticaledgeai.ai
2. Scroll to contact form
3. Fill in test data:
   - Name: `Test User`
   - Email: `test@test.com`
   - Message: `This is a test submission`
4. Click **Send Message**
5. Should see Netlify's default success page

**Verify in Netlify:**
1. Go to Netlify dashboard → **Forms**
2. Click on `contact` form
3. Verify test submission appears

**cURL Test (optional):**
```bash
curl -X POST https://verticaledgeai.ai/ \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "form-name=contact&name=Test&email=test@example.com&message=cURL test"
```

### Step 5.2: Open Graph Image Test

1. Go to https://www.opengraph.xyz/
2. Enter: `https://verticaledgeai.ai`
3. Click **"Fetch"**
4. Verify:
   - Title displays correctly
   - Description displays correctly
   - OG image (1200x630) displays correctly

**Alternative testers:**
- LinkedIn Post Inspector: https://www.linkedin.com/post-inspector/
- Twitter Card Validator: https://cards-dev.twitter.com/validator
- Facebook Sharing Debugger: https://developers.facebook.com/tools/debug/

### Step 5.3: Performance Check

1. Go to https://pagespeed.web.dev/
2. Enter: `https://verticaledgeai.ai`
3. Run analysis
4. Target scores:
   - Performance: >90
   - Accessibility: >90
   - Best Practices: >90
   - SEO: >90

### Step 5.4: Security Headers Check

1. Go to https://securityheaders.com/
2. Enter: `https://verticaledgeai.ai`
3. Review results

**To improve security headers, create `netlify.toml`:**

```toml
[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"
    Content-Security-Policy = "default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com; img-src 'self' data: https:;"
```

### Step 5.5: SSL Certificate Verification

```bash
# Check SSL certificate
curl -vI https://verticaledgeai.ai 2>&1 | grep -A 6 "Server certificate"

# Or use online tool
# https://www.ssllabs.com/ssltest/
```

**✓ CHECKPOINT:** All verification tests pass.

---

## 7. PHASE 6: POST-DEPLOYMENT INTEGRATION

### Step 6.1: Configure Form Notifications

1. Go to Netlify dashboard → **Site settings** → **Forms** → **Form notifications**
2. Click **"Add notification"** → **"Email notification"**
3. Configure:
   - Email to notify: `cordero_ryan@verticaledgeai.ai`
   - Form: `contact`
4. Click **"Save"**

**Optional: Slack Notification**
1. Add notification → **"Slack notification"**
2. Add Slack webhook URL
3. Select form: `contact`

### Step 6.2: Update Email Signature

Add landing page to your professional email signature:

```html
--
Ryan Cordero
Founder, Vertical Edge AI
AI-Powered Business Automation

📧 cordero_ryan@verticaledgeai.ai
🌐 https://verticaledgeai.ai
📅 Book a call: https://cal.com/verticaledgeai/discovery
```

### Step 6.3: Update Cal.com Booking Page

1. Go to https://cal.com/verticaledgeai
2. Edit your event type
3. In **"Confirmation message"** or **"Description"**, add:
   ```
   Learn more about Vertical Edge AI: https://verticaledgeai.ai
   ```

### Step 6.4: Prepare Cold Email Templates

Update your Instantly.ai or Apollo.io email templates to include:

```
# In email body
{{first_name}}, I ran a quick audit on {{company_domain}} and found a few things worth discussing.

See how we help companies like yours: https://verticaledgeai.ai

# In email signature
Ryan Cordero | Vertical Edge AI
https://verticaledgeai.ai
```

### Step 6.5: Connect to VE Platform (Optional)

To capture form submissions in your Vertical Edge platform:

1. Create a Netlify outgoing webhook
2. Point to: `https://vertical-edge-mvp-vv60.onrender.com/api/v1/signals/netlify`
3. Configure to trigger on form submissions

**Webhook Setup:**
1. Netlify → Site settings → Build & deploy → Deploy notifications
2. Add notification → Outgoing webhook
3. Event: Form submission
4. URL: Your VE platform endpoint

---

## 8. TROUBLESHOOTING

### Issue: Form submissions not appearing in Netlify

**Cause:** Form not detected during deploy

**Fix:**
1. Ensure `data-netlify="true"` attribute is on the form
2. Ensure form has a `name` attribute
3. Trigger a new deploy: `git commit --allow-empty -m "trigger rebuild" && git push`

### Issue: DNS not resolving

**Cause:** DNS propagation delay or incorrect records

**Fix:**
1. Wait up to 48 hours for propagation
2. Verify records with: `dig verticaledgeai.ai`
3. Check Netlify dashboard for correct IP/CNAME values
4. Clear local DNS cache:
   - Windows: `ipconfig /flushdns`
   - Mac: `sudo dscacheutil -flushcache`

### Issue: SSL certificate not provisioning

**Cause:** DNS not fully propagated

**Fix:**
1. Wait for DNS to fully propagate
2. In Netlify: Domain management → Click "Renew certificate"
3. Ensure no CAA records blocking Let's Encrypt

### Issue: OG image not displaying

**Cause:** Image not accessible or wrong path

**Fix:**
1. Verify image URL is accessible: `curl -I https://verticaledgeai.ai/assets/images/og-image.png`
2. Ensure `og:image` meta tag has full URL, not relative path
3. Clear social platform cache (use their debug tools)

### Issue: 404 on direct page access

**Cause:** SPA routing issue (not applicable for static site)

**Fix for SPA (if you convert later):**
Add to `netlify.toml`:
```toml
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

---

## 9. REFERENCE LINKS

### Deployment Tools
- GitHub: https://github.com
- Netlify: https://app.netlify.com
- Netlify Docs: https://docs.netlify.com

### Verification Tools
- OG Image Tester: https://www.opengraph.xyz
- PageSpeed Insights: https://pagespeed.web.dev
- Security Headers: https://securityheaders.com
- SSL Test: https://www.ssllabs.com/ssltest

### Asset Generation
- Favicon Generator: https://favicon.io/favicon-generator
- OG Image Templates: https://www.canva.com (search "Open Graph")

### DNS Tools
- DNS Checker: https://dnschecker.org
- DNS Lookup: https://mxtoolbox.com/DNSLookup.aspx

### Vertical Edge Resources
- Main Platform: https://vertical-edge-mvp-vv60.onrender.com
- API Docs: https://vertical-edge-mvp-vv60.onrender.com/docs
- Cal.com Booking: https://cal.com/verticaledgeai/discovery

---

## COMPLETION CHECKLIST

```
PHASE 1: GitHub Setup
[ ] Repository created
[ ] Local git initialized
[ ] Files committed and pushed
[ ] Verified files appear in GitHub

PHASE 2: Netlify Deployment
[ ] Repository connected to Netlify
[ ] Initial deploy successful
[ ] Site accessible at .netlify.app URL

PHASE 3: DNS Configuration
[ ] Custom domain added in Netlify
[ ] A record configured for apex
[ ] CNAME configured for www
[ ] DNS propagated (site loads on custom domain)
[ ] SSL certificate provisioned

PHASE 4: Favicon
[ ] Favicon generated
[ ] Files added to project
[ ] HTML head updated
[ ] Changes pushed and deployed

PHASE 5: Verification
[ ] Form submission test passed
[ ] OG image displays correctly
[ ] Performance score >90
[ ] SSL working (https)

PHASE 6: Integration
[ ] Form notifications configured
[ ] Email signature updated
[ ] Cal.com updated
[ ] Cold email templates updated
```

---

## EXECUTION SUMMARY

```
START → GitHub Push (5m) → Netlify Deploy (3m) → DNS Config (5m) 
     → Favicon (5m, parallel) → Verification (15m) → LIVE

Total: ~35 minutes to fully operational landing page
```

---

**Document Version:** 1.0  
**Generated:** January 28, 2026  
**Protocol:** CITADEL v5 + NEXUS v2.3C  
**Confidence:** 92%  

---

**GO DEPLOY. REPORT BACK WHEN LIVE.**
