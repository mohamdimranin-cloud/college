# FINAL Apps Script Code - Copy This Exactly

## Instructions:
1. Go to https://script.google.com/home
2. Open your script
3. DELETE ALL existing code
4. COPY and PASTE this code:

```javascript
function doPost(e) {
  try {
    // Open the specific spreadsheet and sheet
    var spreadsheet = SpreadsheetApp.openById('1FEcd7U1H6_a-pivu-hDczpWYqhVuTQovVw8LParGWjQ');
    var sheet = spreadsheet.getSheetByName('Sheet1'); // Make sure this matches your sheet name
    
    // If sheet doesn't exist, use the first sheet
    if (!sheet) {
      sheet = spreadsheet.getSheets()[0];
    }
    
    // Get the form data
    var name = e.parameter.Name || '';
    var email = e.parameter.Email || '';
    var phone = e.parameter.Phone || '';
    var message = e.parameter.Message || '';
    var timestamp = new Date().toLocaleString('en-IN', { timeZone: 'Asia/Kolkata' });
    
    // Add headers if this is the first row
    if (sheet.getLastRow() === 0) {
      sheet.appendRow(['Timestamp', 'Name', 'Email', 'Phone', 'Message']);
    }
    
    // Add the data
    sheet.appendRow([timestamp, name, email, phone, message]);
    
    // Return success
    return ContentService
      .createTextOutput(JSON.stringify({status: 'success', message: 'Data saved'}))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    // Log the error
    Logger.log('Error: ' + error.toString());
    
    // Return error
    return ContentService
      .createTextOutput(JSON.stringify({status: 'error', message: error.toString()}))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

// Test function - run this to test if the script works
function testWrite() {
  var spreadsheet = SpreadsheetApp.openById('1FEcd7U1H6_a-pivu-hDczpWYqhVuTQovVw8LParGWjQ');
  var sheet = spreadsheet.getSheetByName('Sheet1');
  
  if (!sheet) {
    sheet = spreadsheet.getSheets()[0];
  }
  
  sheet.appendRow([new Date().toLocaleString(), 'Test Name', 'test@email.com', '1234567890', 'Test message']);
  Logger.log('Test write successful!');
}
```

## After Pasting:

1. Click **Save** (Ctrl+S)
2. **RUN the testWrite function first**:
   - Select "testWrite" from the dropdown at the top
   - Click the ▶️ Run button
   - Authorize if needed
   - Check your sheet - you should see a test row appear!
3. If the test works, then **Deploy**:
   - Click **Deploy** → **Manage deployments**
   - Click **Edit** (pencil icon)
   - Make sure "Who has access" = **Anyone**
   - Click **Update**

## Then test your website form again!

If the testWrite function works but the website form doesn't, we know it's a deployment issue.
If testWrite doesn't work, we know it's a permissions issue.

Let me know what happens!
