# 🚀 Netlify Deployment Checklist - Priority Actions

Based on CITADEL v5 + NEXUS v2.3C analysis, here are the immediate next steps.

## ✅ Completed Actions

- [x] **A1**: Replaced Formspree with Netlify Forms (`data-netlify="true"` added)
- [x] **A2**: Created OG Image (1200x630px) - placeholder ready
- [x] **A3**: Added favicon links to HTML (ready for favicon.io generation)
- [x] **Form Integration**: Netlify Forms with honeypot spam protection configured

## 🔥 Priority Actions (In Order)

### Priority 1: Form Fix ✅ DONE
**Status**: ✅ Complete
- Form now uses `data-netlify="true"`
- Honeypot field added for spam protection
- Form name: `contact`

### Priority 2: Create Favicons (5 min)
**Action**: Generate favicons via https://favicon.io/favicon-generator/

**Settings**:
- **Text**: `VE` (Vertical Edge initials)
- **Background**: Circle
- **Font**: Locker's One (or bold sans-serif)
- **Font Size**: 70
- **Color**: Indigo on white (#4F40E5 indigo, #FFFFFF white)
- **Sizes**: Standard (16x16, 32x32, 48x48)

**Steps**:
1. Go to https://favicon.io/favicon-generator/
2. Enter text "VV"
3. Set background: `#3F3F3F`
4. Set font color: `#FFFFFF`
5. Download and extract to `assets/images/`
6. Files should be: `favicon.ico`, `favicon-16x16.png`, `favicon-32x32.png`

**Note**: HTML already has favicon links configured - just add the files.

### Priority 3: Deploy to Netlify (< 10 min)

#### Step 1: Initialize Git Repository
```bash
cd "c:\Users\Ryan\Documents\Claude 4.5\!!! AI Network - MVP !!!\Landing Page 1.28.26\Landing Page x Cursor Guide"

git init
git add .
git commit -m "Initial commit: Vertical Edge AI landing page with Netlify Forms"
```

#### Step 2: Push to GitHub
**Important**: Use GitHub - better Netlify integration than GitLab.

```bash
# Create repository on GitHub first, then:
git remote add origin https://github.com/YOUR_USERNAME/vertical-edge-landing.git
git branch -M main
git push -u origin main
```

**GitHub Repository Setup**:
1. Go to https://github.com/new
2. Repository name: `vertical-edge-landing`
3. Description: "Vertical Edge AI landing page - production ready"
4. Visibility: Private (or Public)
5. Click "Create repository"

#### Step 3: Connect to Netlify
1. Go to https://app.netlify.com
2. Click "Add new site" → "Import an existing project"
3. Choose "GitHub" (better integration than GitLab)
4. Authorize Netlify access to GitHub
5. Select `vertical-edge-landing` repository

#### Step 4: Configure Build Settings
- **Branch to deploy**: `main`
- **Build command**: (leave empty - static site)
- **Publish directory**: `.` (root)
- Click "Deploy site"

**Expected**: Site deploys in < 3 minutes

### Priority 4: Configure DNS CNAME (5 min)

**Current Status**: Domain email already configured (MX, CNAME, TXT)

**Action Required**: Add CNAME for landing page subdomain

**DNS Configuration**:

**For `www.verticaledgeai.ai` (subdomain)**:
```
Type: CNAME
Name: www
Value: [your-site].netlify.app
```

**For root domain (`verticaledgeai.ai`)**:
```
Type: A
Name: @
Value: [VERIFY IN NETLIFY DASHBOARD - see warning below]
```

**⚠️ CRITICAL DNS NOTE:**

**Verify which IP is correct for Netlify before adding A record:**

| Source | IP Address |
|--------|------------|
| Cursor docs | 75.2.0.85 |
| Netlify official docs | 75.2.60.5 |

**⚠️ IMPORTANT**: Check Netlify's current documentation when you reach Step 3 — they occasionally update load balancer IPs. **The Netlify dashboard will show the correct value when you add your custom domain.**

**When adding custom domain in Netlify**:
1. Go to: Site settings → Domain management → Add custom domain
2. Enter: `verticaledgeai.ai`
3. Netlify will display the **correct A record IP** to use
4. Copy that IP and use it in your DNS provider

**Alternative for `www` (if ALIAS supported)**:
```
Type: ALIAS
Name: www
Value: [your-site].netlify.app
```

**Steps**:
1. In Netlify: Site settings → Domain management
2. Click "Add custom domain"
3. Enter: `www.verticaledgeai.ai`
4. Netlify will show DNS instructions
5. Add CNAME record in your DNS provider:
   - **Type**: CNAME
   - **Name**: `www`
   - **Value**: `[your-site].netlify.app`
6. Wait for DNS propagation (5-60 minutes)

**Note**: Can use Netlify subdomain (`[site].netlify.app`) immediately while DNS propagates.

### Priority 5: Verify SSL Provisioning (Automatic)
**Status**: ✅ Auto-configured by Netlify

Netlify automatically provisions SSL certificates for custom domains. After DNS propagates:
1. Go to Site settings → Domain management → HTTPS
2. Click "Verify DNS configuration"
3. Once verified, SSL is automatically enabled
4. Enable "Force HTTPS" redirect

### Priority 6: Test Contact Form (2 min)
**After deployment**:

**Option 1: Via Browser**:
1. Go to your deployed site
2. Navigate to contact form section
3. Fill out form:
   - Name: Test User
   - Email: test@example.com
   - Message: Test submission
4. Submit form
5. Check Netlify dashboard:
   - Site → Forms → Submissions
   - Should see submission within seconds

**Option 2: Via cURL**:
```bash
curl -X POST https://www.verticaledgeai.ai \
  -d "name=Test User" \
  -d "email=test@example.com" \
  -d "message=Test submission"
```

**Netlify Forms Settings**:
- Go to Site settings → Forms
- Configure email notifications (default: site owner)
- Enable spam filtering (already configured with honeypot)

### Priority 7: Post-Deployment Actions (10 min)

**1. Add to Email Signatures**:
```
---
Vertical Edge AI
Your AI Operations Partner
www.verticaledgeai.ai
```

**2. Update Cal.com Booking Page**:
- Add landing page link to Cal.com event description
- Link: https://cal.com/verticaledgeai/discovery

**3. Test OG Image**:
- Go to: https://www.opengraph.xyz
- Enter: https://www.verticaledgeai.ai
- Verify image displays correctly for social sharing

**4. Share on LinkedIn/Twitter**:
- Post about the launch
- Include landing page URL

## 📊 Risk Mitigation Checklist

- [x] **Form Spam**: Honeypot field added (`bot-field`)
- [x] **OG Image Missing**: Placeholder created (can refine later)
- [x] **DNS Delay**: Use Netlify subdomain initially
- [x] **SSL Issues**: Netlify auto-provisions SSL

## 🎯 Deployment Timeline

| Action | Time | Priority | Status |
|--------|------|----------|--------|
| Form Fix | 2 min | P1 | ✅ Done |
| Favicon Creation | 20 min | P2 | ⏳ Next |
| Git Init + Push | 5 min | P3 | ⏳ Next |
| Netlify Deploy | 3 min | P3 | ⏳ Next |
| DNS CNAME | 5 min | P4 | ⏳ Next |
| SSL Verify | Auto | P5 | ✅ Auto |
| Form Test | 2 min | P6 | ⏳ After deploy |
| Email Signature | 5 min | P7 | ⏳ After deploy |

**Total Time**: ~40 minutes (excluding DNS propagation)

## 🚨 Critical Notes

1. **Don't Block Launch**: Asset polish (favicon, OG image refinement) can happen post-launch
2. **Netlify Forms**: Free tier = 300 submissions/month (sufficient for launch)
3. **DNS Propagation**: Can take 5-60 minutes, use Netlify subdomain in meantime
4. **Form Submissions**: Check Netlify dashboard → Forms → Submissions

## 📝 Post-Deployment Verification

- [ ] Site loads at `[site].netlify.app`
- [ ] Custom domain works (`www.verticaledgeai.ai`)
- [ ] SSL certificate active (HTTPS)
- [ ] Contact form submits successfully
- [ ] Form submission appears in Netlify dashboard
- [ ] Email notification received
- [ ] All images load correctly
- [ ] Mobile responsive design works
- [ ] Page speed < 3 seconds

## 🔗 Quick Links

- **Netlify Dashboard**: https://app.netlify.com
- **Favicon Generator**: https://favicon.io/favicon-generator/
- **GitHub**: https://github.com/new
- **OG Image Tester**: https://www.opengraph.xyz
- **DNS Checker**: https://dnschecker.org

---

**Status**: Ready for deployment  
**Next Step**: Create favicons → Push to GitLab → Deploy to Netlify  
**Estimated Launch**: < 1 hour
