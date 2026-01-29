# Google Apps Script Code

Your Apps Script needs this exact code to work with the contact form.

## Instructions:

1. Go to: https://script.google.com/home
2. Find your script (the one with URL ending in ...0vq34eav/exec)
3. Replace ALL the code with this:

```javascript
function doPost(e) {
  try {
    // Get the spreadsheet
    var sheet = SpreadsheetApp.openById('14Q2cxFBslbW2Ujv-ywFCH9o5b1lfCJg9uwG6hiLhoSQ').getActiveSheet();
    
    // Get parameters
    var params = e.parameter;
    
    // Create timestamp
    var timestamp = new Date().toLocaleString('en-IN', { timeZone: 'Asia/Kolkata' });
    var name = params.Name || '';
    var email = params.Email || '';
    var phone = params.Phone || '';
    var message = params.Message || '';
    
    // Check if headers exist
    if (sheet.getLastRow() === 0) {
      sheet.appendRow(['Timestamp', 'Name', 'Email', 'Phone', 'Message']);
    }
    
    // Append the data
    sheet.appendRow([timestamp, name, email, phone, message]);
    
    // Return success with CORS headers
    return ContentService
      .createTextOutput(JSON.stringify({'status': 'success'}))
      .setMimeType(ContentService.MimeType.JSON);
    
  } catch (error) {
    Logger.log('Error: ' + error.toString());
    return ContentService
      .createTextOutput(JSON.stringify({'status': 'error', 'message': error.toString()}))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

## After Pasting the Code:

1. Click **Save** (disk icon)
2. Click **Deploy** → **Manage deployments**
3. Click the **Edit** icon (pencil) on your existing deployment
4. Make sure:
   - **Execute as:** Me (your email)
   - **Who has access:** Anyone
5. Click **Deploy**
6. Copy the new Web App URL if it changed

## Test Again:

After updating the Apps Script code, try submitting your contact form again. It should work!

## Troubleshooting:

If it still doesn't work:
1. Check the Apps Script execution logs: **Executions** tab in Apps Script
2. Make sure the spreadsheet ID is correct: `14Q2cxFBslbW2Ujv-ywFCH9o5b1lfCJg9uwG6hiLhoSQ`
3. Make sure "Who has access" is set to "Anyone"
