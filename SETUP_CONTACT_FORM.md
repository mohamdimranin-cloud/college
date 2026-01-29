# Contact Form Setup - Quick Guide

## ✅ What's Already Done
Your contact form is ready and configured to work with Google Forms. You just need to complete these 5 simple steps!

## 📋 Step-by-Step Setup (5 minutes)

### Step 1: Create Google Form
1. Go to **https://forms.google.com**
2. Click **+ Blank** to create a new form
3. Give it a title: "Right Guidance PU College - Contact Form"

### Step 2: Add Form Fields
Add these 4 questions in order:

1. **Question 1:**
   - Type: Short answer
   - Question: "Name"
   - Toggle "Required" ON

2. **Question 2:**
   - Type: Short answer
   - Question: "Email"
   - Toggle "Required" ON
   - Click the three dots (⋮) → Response validation
   - Select "Text" → "Email"

3. **Question 3:**
   - Type: Short answer
   - Question: "Phone"
   - Leave "Required" OFF (optional field)

4. **Question 4:**
   - Type: Paragraph
   - Question: "Message"
   - Toggle "Required" ON

### Step 3: Link to Your Google Sheet
1. Click the **Responses** tab at the top
2. Click the green Google Sheets icon
3. Choose **"Select existing spreadsheet"**
4. Find and select your spreadsheet (ID: 14Q2cxFBslbW2Ujv-ywFCH9o5b1lfCJg9uwG6hiLhoSQ)
5. Click **Create**

### Step 4: Get Form ID and Entry IDs

#### Get Form ID:
1. Look at your browser's address bar
2. Copy the form ID from the URL
3. Example URL: `https://docs.google.com/forms/d/1FAIpQLSe_XXXXXXXXXXXXX/edit`
4. The Form ID is: `1FAIpQLSe_XXXXXXXXXXXXX`

#### Get Entry IDs:
1. Click on the **Name** question
2. Look at the URL - you'll see something like `entry.123456789`
3. Write down: Name = `entry.123456789`
4. Repeat for Email, Phone, and Message fields
5. You should have 4 entry IDs like:
   - Name: `entry.123456789`
   - Email: `entry.987654321`
   - Phone: `entry.555555555`
   - Message: `entry.111111111`

### Step 5: Update Your Website Code
1. Open the file **`script.js`** in your website folder
2. Find this section (around line 52):
```javascript
const GOOGLE_FORM_CONFIG = {
    formId: 'YOUR_FORM_ID_HERE',
    fields: {
        name: 'entry.XXXXXXXX',
        email: 'entry.YYYYYYYY',
        phone: 'entry.ZZZZZZZZ',
        message: 'entry.WWWWWWWW'
    }
};
```

3. Replace with your actual values:
```javascript
const GOOGLE_FORM_CONFIG = {
    formId: '1FAIpQLSe_XXXXXXXXXXXXX',  // Your actual form ID
    fields: {
        name: 'entry.123456789',    // Your actual Name entry ID
        email: 'entry.987654321',   // Your actual Email entry ID
        phone: 'entry.555555555',   // Your actual Phone entry ID
        message: 'entry.111111111'  // Your actual Message entry ID
    }
};
```

4. Save the file

## 🧪 Test Your Form

1. Open your website
2. Scroll to the contact form
3. Fill in all fields
4. Click "Send Message"
5. You should see: "Thank you, [Name]! Your message has been received..."
6. Check your Google Sheet - you should see the submission!

## 📊 View Submissions

You can view form submissions in two places:
1. **Google Forms:** Click "Responses" tab to see charts and individual responses
2. **Google Sheet:** All responses are automatically saved to your spreadsheet

## 🎨 Customize (Optional)

### Change Success Message
In `script.js`, find this line:
```javascript
alert(`Thank you, ${name}! Your message has been received. We'll get back to you soon.`);
```
Change the message to whatever you want!

### Change Error Message
Find this line:
```javascript
alert('Sorry, there was an error sending your message. Please try again or contact us directly at info@rightguidance.edu');
```
Update with your actual contact email.

## ❓ Troubleshooting

### "Sending..." button stays forever
- Check that your Form ID and Entry IDs are correct
- Make sure there are no typos in the entry IDs

### Data not appearing in Google Sheet
- Verify the form is linked to the correct Google Sheet
- Check the "Responses" tab in Google Forms to see if data is being received

### Form validation errors
- Make sure Name, Email, and Message are marked as "Required" in Google Forms
- Verify Email field has email validation enabled

## 🎉 You're Done!

Once you complete these steps, your contact form will:
- ✅ Automatically save submissions to your Google Sheet
- ✅ Show a success message to users
- ✅ Reset the form after submission
- ✅ Work reliably and for free forever!

## 📞 Need Help?

If you get stuck on any step, let me know which step number you're on and I'll help you through it!
