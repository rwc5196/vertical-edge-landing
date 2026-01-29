# ✅ AFTER DEPLOYMENT - Verification & Setup

**Come back here once live. I'll help you:**

---

## 1. Verify Form Submissions Are Flowing

### Test Form Submission

**Option A: Via Browser**
1. Visit: https://www.verticaledgeai.ai
2. Navigate to contact form section
3. Fill out form:
   - Name: Test User
   - Email: test@example.com
   - Message: Test submission
4. Submit form

**Option B: Via cURL**
```bash
curl -X POST https://www.verticaledgeai.ai \
  -d "name=Test User" \
  -d "email=test@example.com" \
  -d "message=Test submission"
```

### Check Netlify Forms Dashboard

1. Go to: https://app.netlify.com
2. Select your site
3. Navigate to: **Forms** → **Submissions**
4. **Verify**: Submission appears within seconds
5. **Check**: Form data is captured correctly (name, email, message)

**Expected Result**: Submission appears in dashboard immediately after form submit.

---

## 2. Test OG Image Rendering

### Test Open Graph Image

1. Go to: https://www.opengraph.xyz
2. Enter URL: `https://www.verticaledgeai.ai`
3. Click "Fetch new information"
4. **Verify**:
   - ✅ Image displays correctly (1200x630px)
   - ✅ Title: "Vertical Edge AI | Your AI Operations Partner"
   - ✅ Description shows correctly
   - ✅ Image preview matches your design

### Test on Social Platforms

**LinkedIn**:
- Go to: https://www.linkedin.com/post-inspector/
- Enter: `https://www.verticaledgeai.ai`
- Verify image preview

**Twitter/X**:
- Go to: https://cards-dev.twitter.com/validator
- Enter: `https://www.verticaledgeai.ai`
- Verify card preview

**Facebook**:
- Go to: https://developers.facebook.com/tools/debug/
- Enter: `https://www.verticaledgeai.ai`
- Click "Debug" and verify image

**Expected Result**: OG image displays correctly on all platforms.

---

## 3. Set Up Netlify Form Notifications to Your Email

### Configure Email Notifications

1. Go to: Netlify Dashboard → Your Site → **Site settings**
2. Navigate to: **Forms** → **Form notifications**
3. Click: **Add notification**
4. **Settings**:
   - **Notification type**: Email
   - **Email address**: `cordero_ryan@verticaledgeai.ai`
   - **Event**: Form submission
   - **Form name**: `contact` (matches your form name attribute)
5. Click **Save**

### Test Email Notification

1. Submit a test form on your live site
2. Check email inbox for notification
3. **Verify**: Email received within 1-2 minutes
4. **Verify**: Email contains form submission data

### Optional: Set Up Slack Notifications

1. In Netlify: Forms → Form notifications
2. Click: **Add notification**
3. **Notification type**: Slack webhook
4. **Webhook URL**: [Your Slack webhook URL]
5. **Event**: Form submission
6. Click **Save**

### Optional: Connect to VE Platform

To capture form submissions in your Vertical Edge platform:

1. **Create Netlify Outgoing Webhook**:
   - Go to: Netlify → Site settings → Build & deploy → Deploy notifications
   - Click: **Add notification** → **Outgoing webhook**
   - **Event**: Form submission
   - **URL**: `https://vertical-edge-mvp-vv60.onrender.com/api/v1/signals/netlify`
   - **Form**: `contact`
   - Click **Save**

2. **Verify Integration**:
   - Submit test form on live site
   - Check VE platform dashboard for new signal/lead
   - Verify data mapping is correct

**Expected Result**: Form submissions automatically flow to VE platform for lead processing.

---

## 4. Connect This to Your Outreach Sequence

### Update Email Signature

**Add landing page URL to email signatures:**

```
---
Vertical Edge AI
Your AI Operations Partner
www.verticaledgeai.ai
```

**Or with link**:
```
---
Vertical Edge AI
Your AI Operations Partner
[www.verticaledgeai.ai](https://www.verticaledgeai.ai)
```

### Update Cal.com Booking Confirmation

1. Go to: https://cal.com/verticaledgeai/discovery
2. Navigate to: Event settings → **Confirmation page**
3. Add landing page link:
   ```
   Learn more: www.verticaledgeai.ai
   ```
4. Or add to **Email confirmation**:
   - Include landing page URL in confirmation email template

### Add to Outreach Sequences

**Cold Email Templates**:
- Add landing page URL in email signature
- Reference landing page in follow-up emails
- Use as CTA: "Learn more: www.verticaledgeai.ai"

**LinkedIn Outreach**:
- Add landing page URL to LinkedIn profile
- Include in LinkedIn messages
- Share landing page in posts

**Social Media**:
- Share landing page on LinkedIn
- Post on Twitter/X
- Add to bio links

### Bookmark Netlify Forms Dashboard

**Quick Access**:
- URL: `https://app.netlify.com/sites/[your-site]/forms`
- Bookmark for easy access to new submissions
- Check regularly for lead notifications

---

## 5. Additional Verification Steps

### Performance Check

1. Go to: https://pagespeed.web.dev
2. Enter: `https://www.verticaledgeai.ai`
3. **Target scores**:
   - Performance: >90
   - Accessibility: >95
   - Best Practices: >95
   - SEO: >95

### Security Headers Check

1. Go to: https://securityheaders.com
2. Enter: `https://www.verticaledgeai.ai`
3. **Target**: A or A+ rating

### Mobile Responsiveness

1. Visit site on mobile device
2. Test all sections:
   - Navigation works
   - Forms submit correctly
   - Images load properly
   - Text is readable
   - CTAs are clickable

### SSL Certificate Verification

1. Visit: https://www.verticaledgeai.ai
2. Check browser shows padlock icon
3. Click padlock → Verify certificate details
4. **Verify**: Certificate is valid and issued by Let's Encrypt (via Netlify)

---

## 6. Monitoring Setup

### Set Up Uptime Monitoring (Optional)

**Free Options**:
- **UptimeRobot**: https://uptimerobot.com
  - Monitor: `https://www.verticaledgeai.ai`
  - Alert: Email if site goes down
  - Check interval: 5 minutes

- **Netlify Analytics** (if on paid plan):
  - Site settings → Analytics
  - Enable analytics
  - Track page views, form submissions

### Google Analytics (Optional)

**Add to HTML** (before closing `</head>` tag):
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

## Quick Reference Checklist

**Immediate (Do Now)**:
- [ ] Test form submission
- [ ] Verify submission in Netlify dashboard
- [ ] Test OG image via opengraph.xyz
- [ ] Set up email notifications
- [ ] Update email signature

**Within 24 Hours**:
- [ ] Update Cal.com booking confirmation
- [ ] Share on LinkedIn/Twitter
- [ ] Add to outreach sequences
- [ ] Bookmark Netlify Forms dashboard
- [ ] Run performance check

**Ongoing**:
- [ ] Monitor form submissions daily
- [ ] Check email notifications working
- [ ] Review site analytics weekly
- [ ] Update content as needed

---

## Troubleshooting

### Form Not Submitting

**Check**:
1. Form has `data-netlify="true"` attribute
2. Form has `name="contact"` attribute
3. All required fields have `required` attribute
4. Netlify Forms is enabled (check Site settings)

**Fix**: Verify form HTML matches Netlify Forms requirements.

### Email Notifications Not Working

**Check**:
1. Email address is correct in Netlify settings
2. Check spam folder
3. Verify form name matches notification settings
4. Check Netlify dashboard for errors

**Fix**: Re-configure email notifications in Netlify dashboard.

### OG Image Not Showing

**Check**:
1. Image exists at `/assets/images/og-image.png`
2. Meta tags are correct in HTML
3. Image is accessible (not blocked by CORS)
4. Clear cache and retest

**Fix**: Verify image path and meta tags in HTML.

---

## Success Criteria

✅ **Form submissions**: Flowing correctly  
✅ **OG image**: Rendering on all platforms  
✅ **Email notifications**: Working  
✅ **Outreach integration**: Complete  
✅ **Site performance**: >90 score  
✅ **SSL certificate**: Valid  

**Status**: ✅ All checks passed = Landing page fully operational

---

*You're live. Now let's make sure everything works perfectly.* 🚀
