# 🎨 How to Add Your College Logo

## Quick Steps

### Option 1: Use Your Own Logo File (Recommended)

1. **Save your logo image** in the same folder as `index.html`
   - Supported formats: PNG, JPG, SVG
   - Recommended: PNG with transparent background
   - Suggested size: 200x200px or similar (will auto-resize to 50px height)

2. **Name your logo file**: `logo.png` (or `logo.jpg`, `logo.svg`)

3. **Update the HTML** in `index.html` (around line 98):
   
   Find this line:
   ```html
   <img src="https://i.imgur.com/placeholder-logo.png" alt="Right Guidance PU College Logo" class="logo-image">
   ```
   
   Replace with:
   ```html
   <img src="logo.png" alt="Right Guidance PU College Logo" class="logo-image">
   ```

4. **Done!** Refresh your browser to see your logo.

---

### Option 2: Use an Online Image URL

If your logo is hosted online (like the images you provided):

1. **Copy the image URL** of your logo

2. **Update the HTML** in `index.html` (around line 98):
   
   Replace the `src` with your logo URL:
   ```html
   <img src="YOUR_LOGO_URL_HERE" alt="Right Guidance PU College Logo" class="logo-image">
   ```

   For example, using your first logo:
   ```html
   <img src="https://your-logo-url.png" alt="Right Guidance PU College Logo" class="logo-image">
   ```

---

### Option 3: Create a Logo Folder (Professional)

1. **Create a folder** named `images` in your project

2. **Save your logo** as `images/logo.png`

3. **Update the HTML**:
   ```html
   <img src="images/logo.png" alt="Right Guidance PU College Logo" class="logo-image">
   ```

---

## 🎯 Logo Specifications

### Recommended Sizes:
- **Width**: 150-300px
- **Height**: 150-300px (will auto-resize to 50px in navbar)
- **Format**: PNG with transparent background (best)
- **File size**: Under 100KB for fast loading

### Logo Placement:
- The logo appears in the **top-left** of the navigation bar
- On **mobile devices**, it automatically resizes to 40px height
- The logo is displayed **next to** the college name and location

---

## 🎨 Customizing Logo Size

If you want to change the logo size, edit `styles.css`:

```css
.logo-image {
    height: 50px;  /* Change this value */
    width: auto;
}
```

For mobile:
```css
@media (max-width: 968px) {
    .logo-image {
        height: 40px;  /* Change this value */
    }
}
```

---

## 🔧 Troubleshooting

### Logo not showing?
1. Check the file path is correct
2. Make sure the image file is in the right folder
3. Check the file name matches exactly (case-sensitive)
4. Try opening the image URL directly in browser

### Logo too big or too small?
- Adjust the `height` value in `.logo-image` CSS
- Keep `width: auto` to maintain aspect ratio

### Logo looks blurry?
- Use a higher resolution image (at least 200x200px)
- Use PNG or SVG format for best quality

---

## 📝 Example with Your Logos

Based on the images you showed, here's how to use them:

### For the blue building logo:
```html
<img src="logo-blue.png" alt="Right Guidance PU College Logo" class="logo-image">
```

### For the gradient text logo:
```html
<img src="logo-gradient.png" alt="Right Guidance PU College Logo" class="logo-image">
```

---

## ✨ Current Setup

Your website is already configured to display a logo! Just replace the placeholder URL with your actual logo file path.

**Current code location**: `index.html` - Line 98

**What it looks like now**:
- Logo image (placeholder)
- College name: "Right Guidance PU College"
- Location: "Hangal"

All three elements are displayed together in the navigation bar!

---

**Need help?** Check the CUSTOMIZATION_GUIDE.md for more details.
