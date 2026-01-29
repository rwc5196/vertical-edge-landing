# Vertical Edge AI Landing Page — Cursor Deployment Instructions

## Overview
This document provides step-by-step instructions for deploying the production-ready Vertical Edge AI landing page. Follow these instructions in Cursor to set up, configure, and deploy the site.

---

## Prerequisites Checklist

Before starting, ensure you have:
- [ ] Cursor IDE installed
- [ ] Node.js v18+ installed (`node -v` to check)
- [ ] Git installed (`git -v` to check)
- [ ] GitHub account (for repository hosting)
- [ ] Netlify account (recommended) OR Vercel account
- [ ] Access to verticaledgeai.ai DNS settings (Cloudflare, Namecheap, etc.)
- [ ] Formspree account for contact form (free tier works)

---

## Part 1: Project Setup in Cursor

### Step 1.1: Create Project Directory

Open Cursor terminal (Ctrl+` or Cmd+`) and run:

```bash
# Navigate to your projects directory
cd ~/projects  # or wherever you keep projects

# Create project folder
mkdir vertical-edge-landing
cd vertical-edge-landing

# Initialize git repository
git init
```

### Step 1.2: Create File Structure

Create the following directory structure:

```
vertical-edge-landing/
├── index.html          # Main landing page
├── assets/
│   ├── css/
│   │   └── styles.css  # (optional - CSS is inline in HTML)
│   ├── images/
│   │   ├── og-image.png      # Open Graph image (1200x630)
│   │   └── favicon.ico       # Favicon
│   └── js/
│       └── main.js     # (optional - JS is inline in HTML)
├── _redirects          # Netlify redirects (if using Netlify)
├── netlify.toml        # Netlify configuration
├── vercel.json         # Vercel configuration (if using Vercel)
├── robots.txt          # SEO robots file
├── sitemap.xml         # SEO sitemap
└── README.md           # Project documentation
```

Run in Cursor terminal:

```bash
# Create directories
mkdir -p assets/css assets/images assets/js

# Create empty files
touch index.html _redirects netlify.toml vercel.json robots.txt sitemap.xml README.md
```

---

## Part 2: File Contents

### Step 2.1: index.html

Copy the ENTIRE contents of the optimized landing page HTML into `index.html`.

The file is located at: `/mnt/user-data/outputs/index_optimized.html`

**IMPORTANT**: Before deploying, make these replacements in the HTML:

1. **Formspree Form Action** (Line ~1180):
   - Find: `action="https://formspree.io/f/placeholder"`
   - Replace with your actual Formspree endpoint (see Part 4)

2. **Cal.com Link** (appears 4 times):
   - Current: `https://cal.com/verticaledgeai/discovery`
   - Verify this is correct for your Cal.com setup

3. **Email Address** (footer):
   - Current: `cordero_ryan@verticaledgeai.ai`
   - Verify this is correct

### Step 2.2: netlify.toml

```toml
[build]
  publish = "."
  command = "echo 'No build needed - static HTML'"

[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "DENY"
    X-XSS-Protection = "1; mode=block"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"
    Content-Security-Policy = "default-src 'self'; script-src 'self' 'unsafe-inline' https://fonts.googleapis.com; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com; img-src 'self' data: https:; connect-src 'self' https://formspree.io https://cal.com;"
    Permissions-Policy = "camera=(), microphone=(), geolocation=()"

[[headers]]
  for = "/assets/*"
  [headers.values]
    Cache-Control = "public, max-age=31536000, immutable"

[[headers]]
  for = "/*.html"
  [headers.values]
    Cache-Control = "public, max-age=0, must-revalidate"

[[redirects]]
  from = "https://verticaledgeai.ai/*"
  to = "https://www.verticaledgeai.ai/:splat"
  status = 301
  force = true

[[redirects]]
  from = "/home"
  to = "/"
  status = 301

[[redirects]]
  from = "/index"
  to = "/"
  status = 301
```

### Step 2.3: _redirects (Netlify backup redirects)

```
# Redirect non-www to www (or vice versa - choose one)
https://verticaledgeai.ai/* https://www.verticaledgeai.ai/:splat 301!

# Common redirects
/home / 301
/index / 301
/index.html / 301

# 404 fallback
/* /index.html 200
```

### Step 2.4: vercel.json (if using Vercel instead)

```json
{
  "version": 2,
  "builds": [
    {
      "src": "**/*",
      "use": "@vercel/static"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "headers": {
        "X-Frame-Options": "DENY",
        "X-XSS-Protection": "1; mode=block",
        "X-Content-Type-Options": "nosniff",
        "Referrer-Policy": "strict-origin-when-cross-origin"
      },
      "continue": true
    },
    {
      "src": "/assets/(.*)",
      "headers": {
        "Cache-Control": "public, max-age=31536000, immutable"
      },
      "continue": true
    }
  ],
  "redirects": [
    {
      "source": "/home",
      "destination": "/",
      "permanent": true
    },
    {
      "source": "/index",
      "destination": "/",
      "permanent": true
    }
  ]
}
```

### Step 2.5: robots.txt

```
User-agent: *
Allow: /

Sitemap: https://www.verticaledgeai.ai/sitemap.xml

# Block common bot paths
User-agent: *
Disallow: /api/
Disallow: /admin/
Disallow: /*.json$
```

### Step 2.6: sitemap.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://www.verticaledgeai.ai/</loc>
    <lastmod>2026-01-28</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

### Step 2.7: README.md

```markdown
# Vertical Edge AI Landing Page

Production landing page for Vertical Edge AI - AI-Powered Business Automation.

## Tech Stack
- Pure HTML/CSS/JS (no build step required)
- Google Fonts (Inter, Instrument Serif)
- Formspree for contact form
- Cal.com for booking integration

## Deployment
Deployed on Netlify at: https://www.verticaledgeai.ai

## Local Development
```bash
# Using Python
python -m http.server 8000

# Using Node
npx serve .

# Using PHP
php -S localhost:8000
```

Then open http://localhost:8000

## File Structure
- `index.html` - Main landing page (all CSS/JS inline)
- `netlify.toml` - Netlify configuration
- `_redirects` - Netlify redirect rules
- `robots.txt` - SEO robots file
- `sitemap.xml` - SEO sitemap

## Contact
- Email: cordero_ryan@verticaledgeai.ai
- Booking: https://cal.com/verticaledgeai/discovery

## License
© 2026 Vertical Edge AI LLC. All rights reserved.
```

---

## Part 3: Create Required Assets

### Step 3.1: Favicon

Create a simple favicon. In Cursor terminal:

```bash
# Option 1: Use an online generator
# Go to https://favicon.io/favicon-generator/
# Settings:
#   - Text: "VE"
#   - Background: Rounded
#   - Font Family: Inter
#   - Font Size: 70
#   - Background Color: #4F46E5
#   - Font Color: #FFFFFF
# Download and extract to assets/images/

# Option 2: Create placeholder
echo "<!-- Favicon placeholder -->" > assets/images/favicon.ico
```

### Step 3.2: Open Graph Image

Create an OG image (1200x630px) for social sharing:

**Option A: Use Canva/Figma**
- Dimensions: 1200 x 630 pixels
- Background: #F8FAFC (light) or gradient
- Text: "Vertical Edge AI" + "Your AI Operations Partner"
- Logo if available
- Save as: `assets/images/og-image.png`

**Option B: Add to HTML later**
For now, add this meta tag placeholder in the `<head>` section of index.html:

```html
<meta property="og:image" content="https://www.verticaledgeai.ai/assets/images/og-image.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:image" content="https://www.verticaledgeai.ai/assets/images/og-image.png">
```

---

## Part 4: Formspree Setup

### Step 4.1: Create Formspree Form

1. Go to https://formspree.io
2. Sign up or log in
3. Click "New Form"
4. Settings:
   - Form Name: "Vertical Edge AI Contact"
   - Email: cordero_ryan@verticaledgeai.ai
5. Copy your form endpoint (looks like: `https://formspree.io/f/xyzabcde`)

### Step 4.2: Update HTML

In `index.html`, find and replace:

```html
<!-- FIND THIS -->
<form class="contact-form" action="https://formspree.io/f/placeholder" method="POST">

<!-- REPLACE WITH -->
<form class="contact-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
```

### Step 4.3: Configure Formspree Settings

In Formspree dashboard:
1. Go to Form Settings
2. Enable:
   - Email notifications: ON
   - reCAPTCHA: ON (prevents spam)
   - Custom redirect: `https://www.verticaledgeai.ai/?submitted=true` (optional)
3. Add allowed domains:
   - `verticaledgeai.ai`
   - `www.verticaledgeai.ai`
   - `localhost` (for testing)

---

## Part 5: Git Setup & GitHub

### Step 5.1: Create .gitignore

```bash
# Create .gitignore
cat > .gitignore << 'EOF'
# OS files
.DS_Store
Thumbs.db

# Editor
.vscode/
.idea/
*.swp
*.swo

# Logs
*.log
npm-debug.log*

# Dependencies (if any added later)
node_modules/

# Environment
.env
.env.local
.env.*.local

# Build output (if build step added later)
dist/
build/
.netlify/
.vercel/
EOF
```

### Step 5.2: Initial Commit

```bash
# Stage all files
git add .

# Initial commit
git commit -m "Initial commit: Vertical Edge AI landing page

- Production-ready HTML with inline CSS/JS
- Refined Blue-Teal color scheme
- 10-section content architecture based on competitor research
- Formspree contact form integration
- Cal.com booking integration
- Netlify deployment configuration
- SEO optimizations (robots.txt, sitemap.xml)"
```

### Step 5.3: Create GitHub Repository

```bash
# Create repo on GitHub first, then:
git remote add origin https://github.com/YOUR_USERNAME/vertical-edge-landing.git
git branch -M main
git push -u origin main
```

---

## Part 6: Netlify Deployment

### Step 6.1: Connect to Netlify

1. Go to https://app.netlify.com
2. Click "Add new site" → "Import an existing project"
3. Choose "GitHub"
4. Authorize Netlify to access your GitHub
5. Select `vertical-edge-landing` repository

### Step 6.2: Configure Build Settings

On the deployment configuration screen:
- **Branch to deploy**: `main`
- **Build command**: (leave empty - static site)
- **Publish directory**: `.` (root)
- Click "Deploy site"

### Step 6.3: Configure Custom Domain

After initial deployment:

1. Go to Site settings → Domain management
2. Click "Add custom domain"
3. Enter: `www.verticaledgeai.ai`
4. Follow verification steps

### Step 6.4: DNS Configuration

In your domain registrar (Cloudflare, Namecheap, etc.):

**Option A: Using Netlify DNS (Recommended)**

| Type | Name | Value |
|------|------|-------|
| A | @ | 75.2.60.5 |
| CNAME | www | YOUR-SITE-NAME.netlify.app |

**Option B: Using CNAME (if A record not supported)**

| Type | Name | Value |
|------|------|-------|
| CNAME | www | YOUR-SITE-NAME.netlify.app |
| ALIAS/ANAME | @ | YOUR-SITE-NAME.netlify.app |

### Step 6.5: Enable HTTPS

1. In Netlify: Site settings → Domain management → HTTPS
2. Click "Verify DNS configuration"
3. Once verified, click "Provision certificate"
4. Enable "Force HTTPS"

---

## Part 7: Post-Deployment Verification

### Step 7.1: Functionality Checklist

Run through this checklist after deployment:

```
□ Homepage loads at https://www.verticaledgeai.ai
□ HTTP redirects to HTTPS
□ Non-www redirects to www (or vice versa)
□ All navigation links work
□ "Get Your Free Audit" button opens Cal.com
□ "See How It Works" scrolls to process section
□ Contact form submits successfully
□ Form submission sends email notification
□ All images load correctly
□ Fonts load (Inter, Instrument Serif)
□ Mobile responsive design works
□ Page speed acceptable (<3s load)
```

### Step 7.2: SEO Verification

```bash
# Check robots.txt
curl https://www.verticaledgeai.ai/robots.txt

# Check sitemap
curl https://www.verticaledgeai.ai/sitemap.xml

# Test Open Graph tags
# Go to: https://developers.facebook.com/tools/debug/
# Enter: https://www.verticaledgeai.ai
```

### Step 7.3: Performance Test

1. Go to https://pagespeed.web.dev
2. Enter: https://www.verticaledgeai.ai
3. Target scores:
   - Performance: >90
   - Accessibility: >95
   - Best Practices: >95
   - SEO: >95

### Step 7.4: Security Headers Test

1. Go to https://securityheaders.com
2. Enter: https://www.verticaledgeai.ai
3. Target: A or A+ rating

---

## Part 8: Ongoing Maintenance

### Step 8.1: Making Updates

```bash
# Pull latest changes
git pull origin main

# Make edits in Cursor

# Stage and commit
git add .
git commit -m "Description of changes"

# Push to deploy
git push origin main

# Netlify auto-deploys on push
```

### Step 8.2: Monitoring

Set up monitoring:

1. **Uptime**: Use UptimeRobot (free) or Netlify Analytics
2. **Analytics**: Add Google Analytics or Plausible
3. **Error tracking**: Netlify has built-in form submissions view

### Step 8.3: Adding Analytics (Optional)

Add before closing `</head>` tag in index.html:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

Replace `G-XXXXXXXXXX` with your GA4 measurement ID.

---

## Part 9: Troubleshooting

### Common Issues

**Issue: Form not submitting**
- Check Formspree endpoint URL is correct
- Verify domain is allowed in Formspree settings
- Check browser console for errors

**Issue: Fonts not loading**
- Check Content-Security-Policy allows Google Fonts
- Verify internet connection
- Check for typos in font-family declarations

**Issue: CSS not applying**
- Hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
- Clear Netlify cache: Deploys → Trigger deploy → Clear cache and deploy site

**Issue: Cal.com link not working**
- Verify cal.com/verticaledgeai/discovery is active
- Check for typos in URL

**Issue: Mobile layout broken**
- Check viewport meta tag exists
- Test responsive breakpoints in browser dev tools

---

## Part 10: Quick Reference

### Important URLs

| Resource | URL |
|----------|-----|
| Production Site | https://www.verticaledgeai.ai |
| Netlify Dashboard | https://app.netlify.com |
| Formspree Dashboard | https://formspree.io/forms |
| Cal.com Dashboard | https://cal.com/event-types |
| GitHub Repo | https://github.com/YOUR_USERNAME/vertical-edge-landing |
| PageSpeed Insights | https://pagespeed.web.dev |
| Security Headers | https://securityheaders.com |

### Key Files

| File | Purpose |
|------|---------|
| `index.html` | Main landing page |
| `netlify.toml` | Netlify config & headers |
| `_redirects` | URL redirects |
| `robots.txt` | SEO crawler rules |
| `sitemap.xml` | SEO sitemap |

### Contact Points

| Service | Contact |
|---------|---------|
| Site Email | cordero_ryan@verticaledgeai.ai |
| Booking | cal.com/verticaledgeai/discovery |

---

## Appendix A: Complete index.html Location

The production-ready HTML file is located at:
```
/mnt/user-data/outputs/index_optimized.html
```

Copy this entire file as your `index.html`.

---

## Appendix B: Color Reference

| Element | Hex Code |
|---------|----------|
| Background Primary | #FFFFFF |
| Background Secondary | #F8FAFC |
| Text Primary | #0F172A |
| Text Secondary | #475569 |
| Accent Primary (Indigo) | #4F46E5 |
| Accent Secondary (Teal) | #14B8A6 |
| Border Light | #E2E8F0 |
| Danger/Problem | #EF4444 |
| Success | #22C55E |

---

## Appendix C: Typography Reference

| Element | Font | Weight | Size |
|---------|------|--------|------|
| Headlines (h1, h2, h3) | Instrument Serif | 400 | Responsive |
| Body Text | Inter | 400 | 16px |
| Buttons | Inter | 600 | 15px |
| Labels | Inter | 600-700 | 11-13px |

---

*Document Version: 1.0*
*Last Updated: January 28, 2026*
*For: Vertical Edge AI LLC*
