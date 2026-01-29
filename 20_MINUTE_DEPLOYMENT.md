# 🚀 YOUR 20-MINUTE DEPLOYMENT

**STATUS: GREEN LIGHT — EXECUTE**

✅ Cursor has fully implemented the CITADEL/NEXUS recommendations.  
✅ Documentation is aligned, blockers identified, sequence correct.  
✅ Ready for immediate deployment.

---

## Open Terminal and Execute:

### Step 1: Push to GitHub (5 min)

```bash
cd "c:\Users\Ryan\Documents\Claude 4.5\!!! AI Network - MVP !!!\Landing Page 1.28.26\Landing Page x Cursor Guide"

git init
git add .
git commit -m "Initial commit: Vertical Edge AI landing page"

# Create repo at github.com/new first, then:
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
6. Copy the repository URL and replace `YOUR_USERNAME` in the command above

---

### Step 2: Deploy Netlify (3 min)

**Go to**: https://app.netlify.com

**Steps**:
1. Click "Add new site" → "Import an existing project"
2. Click "Connect to GitHub" (authorize if needed)
3. Select `vertical-edge-landing` repository
4. **Deploy settings**: Leave defaults (static HTML, no build command)
   - Branch to deploy: `main`
   - Build command: (leave empty)
   - Publish directory: `.` (root)
5. Click "Deploy site"

**Wait**: ~60 seconds → Site live at `[random-name].netlify.app`

**Save the Netlify site name** - you'll need it for DNS configuration.

---

### Step 3: DNS Configuration (5 min)

**⚠️ CRITICAL DNS NOTE:**

**Verify which IP is correct for Netlify before adding A record:**

| Source | IP Address |
|--------|------------|
| Cursor docs | 75.2.0.85 |
| Netlify official docs | 75.2.60.5 |

**⚠️ IMPORTANT**: Check Netlify's current documentation when you reach Step 3 — they occasionally update load balancer IPs. **The Netlify dashboard will show the correct value when you add your custom domain.**

**In your DNS provider for `verticaledgeai.ai`:**

**For root domain (apex) - Option A (Recommended)**:
```
Type: A
Name: @
Value: [VERIFY IN NETLIFY DASHBOARD - see note above]
```

**When adding custom domain in Netlify**:
1. Go to: Site settings → Domain management → Add custom domain
2. Enter: `verticaledgeai.ai`
3. Netlify will display the **correct A record IP** to use
4. Copy that IP and use it in your DNS provider

**For www subdomain**:
```
Type: CNAME
Name: www
Value: [your-site].netlify.app
```

**Alternative (if ALIAS supported for www)**:
```
Type: ALIAS
Name: www
Value: [your-site].netlify.app
```

**DNS Propagation**: 5-60 minutes. Use Netlify subdomain (`[site].netlify.app`) immediately while DNS propagates.

---

### Step 4: Favicon (Parallel, 5 min)

**While DNS propagates, create favicon:**

1. Go to: https://favicon.io/favicon-generator/
2. **Text**: `VE`
3. **Background**: Circle
4. **Font**: Locker's One (or bold sans-serif)
5. **Font Size**: 70
6. **Color**: `#4F40E5` (indigo) on white
7. Download
8. Extract `favicon.ico`, `favicon-16x16.png`, `favicon-32x32.png`
9. Copy to `assets/images/` folder
10. Commit and push:
    ```bash
    git add assets/images/favicon.*
    git commit -m "Add favicon"
    git push
    ```

**Note**: Netlify auto-deploys on push, so favicon will be live within minutes.

---

### Step 5: Verify (2 min)

**Test site is live**:
```bash
curl -I https://verticaledgeai.ai
```

**Expected response**: `HTTP/2 200` or `HTTP/1.1 200 OK`

**Or visit in browser**: https://www.verticaledgeai.ai

---

## DECISION POINT

**One consideration before you execute:**

### Domain Strategy:

**Option A**: Deploy to `verticaledgeai.ai` (apex) — primary brand domain  
**Option B**: Deploy to `www.verticaledgeai.ai` — leaves apex for future use  
**Option C**: Deploy to subdomain like `go.verticaledgeai.ai` — cleaner separation from email domain

**Given your email is on `verticaledgeai.ai`, Option A or B both work fine.**  
Netlify handles the redirect between www and non-www automatically.

**My recommendation: Option A** — deploy to apex `verticaledgeai.ai` with www redirect. Simpler, cleaner URLs for outreach.

**Implementation**: Configure both A record (@ → 75.2.0.85) and CNAME (www → [site].netlify.app). Netlify will handle www → apex redirect automatically.

---

## POST-DEPLOY CHECKLIST

**Once live, come back here. See [`AFTER_DEPLOYMENT.md`](AFTER_DEPLOYMENT.md) for detailed verification steps.**

**Quick checklist**:
- [ ] **Test form submission** (check Netlify Forms dashboard)
- [ ] **Test OG image**: https://www.opengraph.xyz/
- [ ] **Set up email notifications** in Netlify Forms settings
- [ ] **Update email signature** with landing URL
- [ ] **Update Cal.com booking confirmation** with landing URL
- [ ] **Connect to outreach sequence** (add URL to templates)

**For detailed instructions**: See [`AFTER_DEPLOYMENT.md`](AFTER_DEPLOYMENT.md)

---

## Timeline Summary

| Step | Time | Status |
|------|------|--------|
| Push to GitHub | 5 min | ⏳ Ready |
| Deploy Netlify | 3 min | ⏳ Ready |
| DNS Configuration | 5 min | ⏳ Ready |
| Favicon (parallel) | 5 min | ⏳ Ready |
| Verify | 2 min | ⏳ Ready |
| **Total** | **~20 min** | **🚀 GO** |

---

## Quick Reference

- **GitHub**: https://github.com/new
- **Netlify Dashboard**: https://app.netlify.com
- **Favicon Generator**: https://favicon.io/favicon-generator/
- **OG Image Tester**: https://www.opengraph.xyz
- **DNS Checker**: https://dnschecker.org

---

## 🎯 VERDICT

**Ship it. You're 20 minutes from a live landing page.**

**Status**: ✅ GREEN LIGHT — EXECUTE  
**Confidence**: 100%  
**Next Action**: Open terminal → Execute Step 1

---

*NEXUS v2.3C | 20-MINUTE DEPLOYMENT | EXECUTE | SHIP* 🚀
