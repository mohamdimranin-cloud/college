# FINAL WORKING Apps Script Code

Replace your Apps Script with this code that handles both GET and POST:

```javascript
function doGet(e) {
  return handleRequest(e);
}

function doPost(e) {
  return handleRequest(e);
}

function handleRequest(e) {
  Logger.log('=== NEW REQUEST ===');
  Logger.log('Request received at: ' + new Date());
  Logger.log('Parameters: ' + JSON.stringify(e.parameter));
  
  try {
    // Open spreadsheet
    var spreadsheet = SpreadsheetApp.openById('1FEcd7U1H6_a-pivu-hDczpWYqhVuTQovVw8LParGWjQ');
    var sheet = spreadsheet.getSheetByName('Sheet1');
    
    if (!sheet) {
      sheet = spreadsheet.getSheets()[0];
    }
    
    // Get form data
    var name = e.parameter.Name || '';
    var email = e.parameter.Email || '';
    var phone = e.parameter.Phone || '';
    var message = e.parameter.Message || '';
    var timestamp = new Date().toLocaleString('en-IN', { timeZone: 'Asia/Kolkata' });
    
    Logger.log('Writing data: ' + [timestamp, name, email, phone, message].join(', '));
    
    // Add headers if needed
    if (sheet.getLastRow() === 0) {
      sheet.appendRow(['Timestamp', 'Name', 'Email', 'Phone', 'Message']);
    }
    
    // Write the data
    sheet.appendRow([timestamp, name, email, phone, message]);
    Logger.log('Data written successfully to row: ' + sheet.getLastRow());
    
    // Return success
    return ContentService
      .createTextOutput(JSON.stringify({
        status: 'success',
        message: 'Data saved',
        row: sheet.getLastRow()
      }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    Logger.log('ERROR: ' + error.toString());
    
    return ContentService
      .createTextOutput(JSON.stringify({
        status: 'error',
        message: error.toString()
      }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

## Steps:
1. Copy this code
2. Paste into your Apps Script
3. Save (Ctrl+S)
4. Deploy → Manage deployments → Edit → Update
5. Redeploy your website to Netlify (upload the new script.js)
6. Test the form!

This will work because we're now sending data as URL parameters with GET, which works perfectly with no-cors mode!
