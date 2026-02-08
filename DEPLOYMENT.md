# Vertical Edge AI — Landing Page Deployment

Single reference for Netlify setup, custom domain, form config, and platform webhook.

---

## 1. Netlify Setup

1. **Connect repo:** https://app.netlify.com → Add new site → Import from Git → GitHub → `vertical-edge-landing`
2. **Build settings:** Leave defaults (static HTML; no build command; publish directory: `.`)
3. **Branch:** `main`
4. **Deploy** — site will be live at `[site-name].netlify.app`

---

## 2. Custom Domain (verticaledgeai.ai)

**DNS (at your registrar for verticaledgeai.ai):**

- **Apex:** Type `A`, Name `@`, Value = IP shown in Netlify when you add the domain (verify in Netlify dashboard; they update IPs).
- **www:** Type `CNAME`, Name `www`, Value `[your-site].netlify.app`

**In Netlify:** Site settings → Domain management → Add custom domain → add `verticaledgeai.ai` and `www.verticaledgeai.ai`. Netlify provisions SSL.

**Redirect:** Apex → www is configured in `_redirects`: `https://verticaledgeai.ai/*` → `https://www.verticaledgeai.ai/:splat` (301).

---

## 3. Form Config (Netlify Forms)

- Form uses `data-netlify="true"`; no Formspree. Submissions appear in Netlify → Forms → Submissions.
- **Email notifications:** Site settings → Forms → Form notifications → Add notification → Email → `cordero_ryan@verticaledgeai.ai`, event: Form submission.
- **Optional — connect to VE platform:** Site settings → Build & deploy → Deploy notifications → Add notification → Outgoing webhook:
  - **Event:** Form submission  
  - **URL:** `https://vertical-edge-mvp-vv60.onrender.com/api/v1/signals/netlify`  
  - **Form:** `contact`

---

## 4. Important URLs

| Resource        | URL |
|-----------------|-----|
| Production site | https://www.verticaledgeai.ai |
| Cal.com booking | https://cal.com/verticaledgeai/discovery |
| Contact email   | cordero_ryan@verticaledgeai.ai |

---

## 5. Verify After Deploy

```bash
curl -I https://www.verticaledgeai.ai
# Expect HTTP/2 200 or 301
```

- **Form:** Submit test on site; check Netlify Forms dashboard.
- **OG image:** https://www.opengraph.xyz → enter `https://www.verticaledgeai.ai`

---

## 6. Security Headers

Defined in `netlify.toml`: X-Frame-Options, X-XSS-Protection, X-Content-Type-Options, Referrer-Policy, Content-Security-Policy, Permissions-Policy. No change needed unless you add new origins.
