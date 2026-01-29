# 🎨 Customization Guide - Right Guidance PU College Website

This guide will help you customize the website to match your college's specific needs.

## 📝 Quick Customization Checklist

### 1. Contact Information
**File:** `index.html`

Replace these placeholders throughout the file:
- `[phone_number]` → Your actual phone number (e.g., 9876543210)
- `info@rightguidancepuc.edu` → Your actual email
- Update address in Contact section and Footer

**Locations to update:**
- Line ~60: Meta tags (Schema.org)
- Line ~170: Hero section WhatsApp button
- Line ~650: Contact section
- Line ~750: Footer section

### 2. College Name & Location
**File:** `index.html`

If your college has a different name:
- Search and replace "Right Guidance PU College" with your college name
- Update "Hangal" with your city name
- Update geo coordinates in meta tags (Line ~40)

### 3. Statistics & Numbers
**File:** `index.html` (About Section, Line ~250)

Update these numbers to match your college:
```html
<h3 class="stat-number">500+</h3> <!-- Total students -->
<h3 class="stat-number">95%</h3>  <!-- Success rate -->
<h3 class="stat-number">25+</h3>  <!-- Faculty count -->
<h3 class="stat-number">10+</h3>  <!-- Years of experience -->
<h3 class="stat-number">5000+</h3> <!-- Library books -->
<h3 class="stat-number">100+</h3> <!-- Toppers -->
```

### 4. Course Details
**File:** `index.html` (Courses Section, Line ~280)

Update for each course card:
- Course descriptions
- Features list
- Statistics (NEET/JEE rates, student count)
- Course badges ("Most Popular", "High Demand", etc.)

### 5. Achievements
**File:** `index.html` (Achievements Section, Line ~550)

Customize achievement cards:
- Award names and descriptions
- Years
- Statistics
- Icons (use emojis or replace with images)

### 6. Fee Structure
**File:** `index.html` (FAQ Section, Line ~650)

Update the fee information in FAQ:
```html
<p>Annual fees range from ₹25,000 to ₹35,000...</p>
```

### 7. Images

#### Replace Course Images:
**File:** `index.html` (Lines ~290-380)

Current images use Unsplash. To use your own:
```html
<!-- Replace this URL -->
<img src="https://images.unsplash.com/photo-xxx" alt="...">

<!-- With your image -->
<img src="images/science-lab.jpg" alt="Science Lab">
```

#### Image Locations:
- Course cards: 4 images
- Gallery section: 6 images
- Why Choose Us: 6 images
- Testimonials: 4 profile images
- About section: 1 hero image

**Recommended Image Sizes:**
- Course cards: 400x250px
- Gallery: 500x400px
- Why Choose Us: 300x200px
- Testimonials: 100x100px (circular)
- About hero: 600x400px

### 8. Colors & Branding
**File:** `styles.css` (Lines 1-20)

Change the color scheme:
```css
:root {
    --primary-color: #6366f1;    /* Main brand color */
    --accent-color: #ec4899;     /* Secondary accent */
    --secondary-color: #f59e0b;  /* Tertiary color */
    --success-color: #10b981;    /* Success messages */
}
```

**Popular Color Schemes:**
- Blue & Orange: `#2563eb` & `#f97316`
- Green & Yellow: `#10b981` & `#fbbf24`
- Purple & Pink: `#8b5cf6` & `#ec4899`
- Red & Gold: `#ef4444` & `#f59e0b`

### 9. Testimonials
**File:** `index.html` (Testimonials Section, Line ~480)

Update each testimonial:
- Student name
- Course/College
- Achievement badge
- Testimonial text
- Profile image

### 10. Social Media Links
**File:** `index.html` (Footer Section, Line ~760)

Add your social media URLs:
```html
<div class="social-links">
    <a href="https://facebook.com/yourpage">📘</a>
    <a href="https://instagram.com/yourpage">📷</a>
    <a href="https://twitter.com/yourpage">🐦</a>
    <a href="https://youtube.com/yourchannel">📺</a>
</div>
```

## 🎯 Advanced Customization

### Add New Section

1. **HTML Structure:**
```html
<section class="your-section">
    <div class="container">
        <div class="section-header">
            <h2 class="section-title">Your Title</h2>
            <p class="section-subtitle">Your Subtitle</p>
        </div>
        <!-- Your content here -->
    </div>
</section>
```

2. **Add CSS:**
```css
.your-section {
    background: linear-gradient(180deg, #ffffff 0%, #f0f9ff 100%);
    padding: 5rem 0;
}
```

### Change Fonts

**File:** `styles.css` (Line ~30)

```css
body {
    font-family: 'Your Font', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}
```

Add Google Fonts in `index.html` `<head>`:
```html
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800&display=swap" rel="stylesheet">
```

### Add Logo

**File:** `index.html` (Line ~110)

Replace text logo with image:
```html
<div class="logo">
    <img src="images/logo.png" alt="Right Guidance PU College" class="logo-image">
    <span class="location">Hangal</span>
</div>
```

**File:** `styles.css`

Add logo styling:
```css
.logo-image {
    height: 50px;
    width: auto;
}
```

### Enable Google Analytics

**File:** `index.html` (Before `</head>`)

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

Replace `GA_MEASUREMENT_ID` with your actual ID.

### Add WhatsApp Chat Widget

Already included! Update the phone number:
**File:** `index.html` (Line ~800)

```html
<a href="https://wa.me/919876543210" class="whatsapp-float">
```

## 📱 Testing Checklist

After customization, test:

- [ ] All links work correctly
- [ ] Contact form submits properly
- [ ] Images load on all devices
- [ ] Mobile menu opens/closes
- [ ] FAQ accordion works
- [ ] Smooth scrolling functions
- [ ] WhatsApp button opens correctly
- [ ] All phone numbers are correct
- [ ] Email addresses are valid
- [ ] Social media links work
- [ ] Statistics display correctly
- [ ] Responsive on mobile/tablet/desktop

## 🚀 Deployment

### Option 1: GitHub Pages (Free)
1. Create GitHub repository
2. Upload all files
3. Go to Settings → Pages
4. Select main branch
5. Your site will be live at `username.github.io/repo-name`

### Option 2: Netlify (Free)
1. Sign up at netlify.com
2. Drag and drop your folder
3. Site goes live instantly
4. Custom domain available

### Option 3: Traditional Hosting
1. Upload files via FTP
2. Ensure index.html is in root
3. Set proper file permissions
4. Test all functionality

## 🔧 Troubleshooting

**Images not loading?**
- Check file paths are correct
- Ensure images are in correct folder
- Verify image file names match HTML

**Colors not changing?**
- Clear browser cache (Ctrl+Shift+R)
- Check CSS variable names
- Ensure no typos in color codes

**Mobile menu not working?**
- Check script.js is loaded
- Verify no JavaScript errors in console
- Test on actual mobile device

**Form not submitting?**
- Add backend form handler
- Use services like Formspree or Netlify Forms
- Or connect to your email server

## 📞 Support

For customization help:
- Check README.md for features
- Review code comments
- Test on multiple browsers
- Use browser DevTools for debugging

## 🎓 Best Practices

1. **Optimize Images:** Use WebP format, compress before upload
2. **Test Regularly:** Check on different devices and browsers
3. **Keep Backups:** Save original files before editing
4. **Update Content:** Keep information current and accurate
5. **Monitor Performance:** Use Google PageSpeed Insights
6. **SEO:** Update meta tags for your college
7. **Accessibility:** Ensure all images have alt text
8. **Security:** Use HTTPS for live site

---

**Last Updated:** January 2025
**Version:** 1.0.0
