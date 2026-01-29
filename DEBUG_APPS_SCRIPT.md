
# Debug Apps Script - Use This to Find the Problem

Replace your Apps Script code with this version that has detailed logging:

```javascript
function doGet(e) {
  return handleRequest(e);
}

function doPost(e) {
  // Although the user's request was a GET, it's good practice to handle POST if data submission is expected.
  // The provided example uses URL parameters which are typical for GET, but forms often submit via POST.
  return handleRequest(e);
}

function handleRequest(e) {
  // Use console.log for better logging and integration with Cloud Logging (Stackdriver)
  console.log('=== NEW REQUEST ===');
  console.log('Request received at: ' + new Date());
  console.log('Parameters: ' + JSON.stringify(e.parameter));
  
  try {
    // Open spreadsheet
    // It's generally safer to ensure the spreadsheet ID is valid and accessible.
    var spreadsheetId = '1FEcd7U1H6_a-pivu-hDczpWYqhVuTQovVw8LParGWjQ'; 
    var spreadsheet = SpreadsheetApp.openById(spreadsheetId);
    var sheet = spreadsheet.getSheetByName('Sheet1');
    
    // If 'Sheet1' doesn't exist, try to get the first sheet or throw an error.
    if (!sheet) {
      var sheets = spreadsheet.getSheets();
      if (sheets.length > 0) {
        sheet = sheets[0];
        console.log('Sheet1 not found, using the first available sheet: ' + sheet.getName());
      } else {
        throw new Error('No sheets found in the spreadsheet.');
      }
    }
    
    // Get form data
    var name = e.parameter.Name || '';
    var email = e.parameter.Email || '';
    var phone = e.parameter.Phone || '';
    var message = e.parameter.Message || '';
    var timestamp = new Date().toLocaleString('en-IN', { timeZone: 'Asia/Kolkata' });
    
    console.log('Attempting to write data: ' + [timestamp, name, email, phone, message].join(', '));
    
    // Define the header row and the data row
    var headerRow = ['Timestamp', 'Name', 'Email', 'Phone', 'Message'];
    var dataRow = [timestamp, name, email, phone, message];
    
    // Prepare an array to hold all rows to be written in one go
    var rowsToWrite = [];
    
    // Check if headers need to be added (if the sheet is empty)
    var lastRow = sheet.getLastRow();
    if (lastRow === 0) {
      rowsToWrite.push(headerRow);
    }
    
    // Add the current data row
    rowsToWrite.push(dataRow);
    
    // Determine the starting row for the write operation
    // If headers were added, it starts at row 1 (A1). If not, it starts at lastRow + 1.
    var startRow = (lastRow === 0) ? 1 : lastRow + 1;
    
    // Write all rows (headers + data) in a single batch operation
    sheet.getRange(startRow, 1, rowsToWrite.length, rowsToWrite[0].length).setValues(rowsToWrite);
    
    // Get the new last row after the write operation
    var newLastRow = sheet.getLastRow();
    console.log('Data written successfully. New last row is: ' + newLastRow);
    
    // Return success
    return ContentService
      .createTextOutput(JSON.stringify({
        status: 'success',
        message: 'Data saved',
        row: newLastRow // Return the actual row where the data was written
      }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    console.error('ERROR: ' + error.toString()); // Use console.error for errors
    
    return ContentService
      .createTextOutput(JSON.stringify({
        status: 'error',
        message: error.toString()
      }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

```

## After Updating:

1. Save the script
2. Deploy → Manage deployments → Edit → Update
3. Submit your website form again
4. Go to **Executions** tab in Apps Script
5. Click on the latest execution
6. Look at the logs - they will tell you exactly what's happening

The logs will show:
- If the request is being received
- What data is being sent
- If there are any errors
- Which row the data was written to

Share the logs with me and we'll fix it!
