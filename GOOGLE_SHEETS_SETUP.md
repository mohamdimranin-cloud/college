# Google Sheets Integration Setup Guide

## Overview
This guide will help you connect your contact form to your Google Sheets spreadsheet so that form submissions are automatically saved.

## Your Google Sheet
**Spreadsheet URL:** https://docs.google.com/spreadsheets/d/14Q2cxFBslbW2Ujv-ywFCH9o5b1lfCJg9uwG6hiLhoSQ/edit?usp=drivesdk

## Setup Steps

### Step 1: Prepare Your Google Sheet
1. Open your Google Sheet using the URL above
2. Create a new sheet (tab) called "Contact Form Submissions" or rename the first sheet
3. Add the following headers in the first row:
   - Column A: **Timestamp**
   - Column B: **Name**
   - Column C: **Email**
   - Column D: **Phone**
   - Column E: **Message**

### Step 2: Create Google Apps Script
1. In your Google Sheet, click on **Extensions** → **Apps Script**
2. Delete any existing code in the script editor
3. Copy and paste the following code:

```javascript
function doPost(e) {
  try {
    // Get the active spreadsheet
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Contact Form Submissions');
    
    // If sheet doesn't exist, create it
    if (!sheet) {
      sheet = SpreadsheetApp.getActiveSpreadsheet().insertSheet('Contact Form Submissions');
      // Add headers
      sheet.appendRow(['Timestamp', 'Name', 'Email', 'Phone', 'Message']);
    }
    
    // Get form data
    var timestamp = new Date();
    var name = e.parameter.Name || '';
    var email = e.parameter.Email || '';
    var phone = e.parameter.Phone || '';
    var message = e.parameter.Message || '';
    
    // Append data to sheet
    sheet.appendRow([timestamp, name, email, phone, message]);
    
    // Return success response
    return ContentService.createTextOutput(JSON.stringify({
      'status': 'success',
      'message': 'Data saved successfully'
    })).setMimeType(ContentService.MimeType.JSON);
    
  } catch (error) {
    // Return error response
    return ContentService.createTextOutput(JSON.stringify({
      'status': 'error',
      'message': error.toString()
    })).setMimeType(ContentService.MimeType.JSON);
  }
}
```

4. Click **Save** (disk icon) and give your project a name like "Contact Form Handler"

### Step 3: Deploy as Web App
1. Click on **Deploy** → **New deployment**
2. Click the gear icon ⚙️ next to "Select type" and choose **Web app**
3. Configure the deployment:
   - **Description:** Contact Form Submission Handler
   - **Execute as:** Me (your email)
   - **Who has access:** Anyone
4. Click **Deploy**
5. You may need to authorize the script:
   - Click **Authorize access**
   - Choose your Google account
   - Click **Advanced** → **Go to [Project Name] (unsafe)**
   - Click **Allow**
6. **IMPORTANT:** Copy the **Web app URL** that appears (it will look like: `https://script.google.com/macros/s/AKfycby.../exec`)

### Step 4: Update Your Website Code
1. Open the `script.js` file in your website
2. Find this line:
   ```javascript
   const response = await fetch('YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL', {
   ```
3. Replace `'YOUR_GOOGLE_APPS_SCRIPT_WEB_APP_URL'` with your actual Web App URL (keep the quotes)
4. Example:
   ```javascript
   const response = await fetch('https://script.google.com/macros/s/AKfycby.../exec', {
   ```

### Step 5: Test the Form
1. Open your website
2. Fill out the contact form
3. Click "Send Message"
4. Check your Google Sheet - you should see a new row with the submitted data

## Troubleshooting

### Form submission fails
- Make sure you deployed the script as a Web App (not just saved it)
- Verify the Web App URL is correct in `script.js`
- Check that "Who has access" is set to "Anyone" in the deployment settings

### Data not appearing in sheet
- Make sure the sheet name is exactly "Contact Form Submissions"
- Check the Apps Script execution logs: In Apps Script editor, click **Executions** on the left sidebar

### Authorization issues
- You may need to re-authorize the script if you see permission errors
- Go to Apps Script → Deploy → Manage deployments → Edit → Re-authorize

## Alternative: Using Google Forms (Simpler Option)

If the above seems complex, you can use Google Forms as an alternative:

1. Create a Google Form with fields: Name, Email, Phone, Message
2. Link it to your Google Sheet (Responses → Link to Sheets)
3. Get the form's pre-filled link
4. Update your HTML form to submit to the Google Form

Would you like instructions for the Google Forms method instead?

## Security Notes
- The Web App URL is public but only accepts POST requests
- Consider adding reCAPTCHA to prevent spam submissions
- You can add email notifications in the Apps Script to get notified of new submissions

## Need Help?
If you encounter any issues during setup, please let me know which step you're stuck on!
