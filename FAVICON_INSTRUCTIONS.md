# Favicon Creation Instructions

## Quick Setup via favicon.io

### Step 1: Generate Favicon
1. Go to https://favicon.io/favicon-generator/
2. **Text**: Enter `VE` (Vertical Edge initials)
3. **Background**: Circle
4. **Font Family**: Leckerli One (or any bold sans-serif)
5. **Font Size**: 70
6. **Font Color**: #FFFFFF (white)
7. **Background Color**: #4F40E5 (indigo — matches brand)
7. Click "Download"

### Step 2: Extract Files
The download will include:
- `favicon.ico` (main favicon) ✅ **Required**
- `favicon-16x16.png` ✅ **Required**
- `favicon-32x32.png` ✅ **Required**
- `apple-touch-icon.png` ✅ **Required** (for iOS)
- `android-chrome-192x192.png` ✅ **Required** (for Android)
- `android-chrome-512x512.png` ✅ **Required** (for Android)
- `site.webmanifest` (optional)

### Step 3: Copy to Project
Copy these files to:
```
assets/images/
├── favicon.ico
├── favicon-16x16.png
└── favicon-32x32.png
```

### Step 4: Update HTML Head
Add these lines to the `<head>` section of `index.html` (if not already present):

```html
<!-- Favicon -->
<link rel="apple-touch-icon" sizes="180x180" href="/assets/images/apple-touch-icon.png">
<link rel="icon" type="image/png" sizes="32x32" href="/assets/images/favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="/assets/images/favicon-16x16.png">
<link rel="icon" type="image/x-icon" href="/assets/images/favicon.ico">
```

**Note**: Some favicon links may already be in HTML - verify all are present.

## Alternative: Manual Creation

If you prefer to create manually:

1. **Design**: Create 32x32px image with "VV" text
2. **Convert**: Use online converter (e.g., https://convertio.co/png-ico/)
3. **Save**: As `favicon.ico`
4. **Copy**: To `assets/images/` folder

## Testing

After deployment:
1. Visit your site
2. Check browser tab - should show "VV" favicon
3. If not visible, hard refresh (Ctrl+Shift+R)

---

**Time Required**: ~5 minutes  
**Priority**: Medium (can be done post-launch)
