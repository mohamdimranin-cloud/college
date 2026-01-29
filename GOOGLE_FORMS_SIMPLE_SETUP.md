# Simple Google Forms Integration (Easier Alternative)

This is a simpler method that doesn't require any coding in Google Apps Script.

## Step 1: Create a Google Form

1. Go to https://forms.google.com
2. Click **+ Blank** to create a new form
3. Title it "Right Guidance PU College - Contact Form"
4. Add the following questions:
   - **Name** (Short answer, Required)
   - **Email** (Short answer, Required, Email validation)
   - **Phone** (Short answer, Optional)
   - **Message** (Paragraph, Required)

## Step 2: Link Form to Your Google Sheet

1. In your Google Form, click the **Responses** tab
2. Click the Google Sheets icon (green icon with white cross)
3. Choose "Select existing spreadsheet"
4. Select your spreadsheet: `14Q2cxFBslbW2Ujv-ywFCH9o5b1lfCJg9uwG6hiLhoSQ`
5. Click **Create**

## Step 3: Get the Form Submit URL

1. In your Google Form, click **Send** (top right)
2. Click the **<>** (link/embed) icon
3. Copy the form URL (it will look like: `https://docs.google.com/forms/d/e/FORM_ID/viewform`)
4. Modify it to get the submit URL by replacing `/viewform` with `/formResponse`
5. Example: `https://docs.google.com/forms/d/e/FORM_ID/formResponse`

## Step 4: Get Field Names

1. Open your form in edit mode
2. Click on the first question (Name)
3. Look at the URL - you'll see something like `entry.123456789`
4. Note down the entry IDs for each field:
   - Name: `entry.XXXXXXXX`
   - Email: `entry.YYYYYYYY`
   - Phone: `entry.ZZZZZZZZ`
   - Message: `entry.WWWWWWWW`

## Step 5: Update Your Website Code

Replace the form submission code in `script.js` with this simpler version:

```javascript
// Simple Google Forms submission
const contactForm = document.getElementById('contactForm');

contactForm.addEventListener('submit', async (e) => {
    e.preventDefault();
    
    const submitButton = contactForm.querySelector('button[type="submit"]');
    const originalButtonText = submitButton.textContent;
    
    submitButton.disabled = true;
    submitButton.textContent = 'Sending...';
    
    const name = document.getElementById('name').value;
    const email = document.getElementById('email').value;
    const phone = document.getElementById('phone').value;
    const message = document.getElementById('message').value;
    
    // Replace these entry IDs with your actual form field IDs
    const formData = new URLSearchParams({
        'entry.XXXXXXXX': name,      // Replace with your Name field ID
        'entry.YYYYYYYY': email,     // Replace with your Email field ID
        'entry.ZZZZZZZZ': phone,     // Replace with your Phone field ID
        'entry.WWWWWWWW': message    // Replace with your Message field ID
    });
    
    try {
        // Replace FORM_ID with your actual form ID
        await fetch('https://docs.google.com/forms/d/e/FORM_ID/formResponse', {
            method: 'POST',
            mode: 'no-cors',
            headers: {
                'Content-Type': 'application/x-www-form-urlencoded'
            },
            body: formData.toString()
        });
        
        alert(`Thank you, ${name}! Your message has been received. We'll get back to you soon.`);
        contactForm.reset();
        
    } catch (error) {
        console.error('Error:', error);
        alert('Sorry, there was an error sending your message. Please try again.');
    } finally {
        submitButton.disabled = false;
        submitButton.textContent = originalButtonText;
    }
});
```

## Step 6: Test

1. Fill out your website's contact form
2. Submit it
3. Check your Google Sheet - you should see the response appear

## Advantages of This Method
- ✅ No Apps Script coding required
- ✅ Automatic spam protection from Google
- ✅ Built-in data validation
- ✅ Can view responses in both Forms and Sheets
- ✅ Easy to modify form fields

## Note
The `mode: 'no-cors'` means you won't get a response back from Google, but the data will still be submitted successfully. This is a limitation of Google Forms but it works reliably.

## Which Method Should You Use?

**Use Google Forms (this method) if:**
- You want the simplest setup
- You don't need custom response handling
- You're okay with not getting confirmation from the server

**Use Apps Script (other method) if:**
- You need full control over the submission process
- You want custom error handling
- You need to send confirmation emails
- You want to integrate with other services

Let me know which method you'd prefer and I can help you set it up!
