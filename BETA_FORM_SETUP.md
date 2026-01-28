# Beta Signup Form Setup Guide

This guide explains how to set up the Google Sheets backend to collect beta tester signups from your FragIQ landing page.

## Overview

The form submits data to a Google Apps Script web app, which saves entries to a private Google Sheet. Only you have access to the data.

---

## Step 1: Create a Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new spreadsheet
3. Name it something like "FragIQ Beta Signups"
4. In **Row 1**, add these headers (in columns A through K):

| A | B | C | D | E | F | G | H | I | J | K |
|---|---|---|---|---|---|---|---|---|---|---|
| Timestamp | Email | Device Model | Android Version | Experience Level | Use Cases | Competitor Apps | 14-Day Commitment | Feedback Commitment | Feedback Channel | Testing Interests |

5. **Copy the Sheet ID** from the URL:
   - URL looks like: `https://docs.google.com/spreadsheets/d/`**`YOUR_SHEET_ID_HERE`**`/edit`
   - The Sheet ID is the long string between `/d/` and `/edit`

---

## Step 2: Create the Google Apps Script

1. Go to [Google Apps Script](https://script.google.com)
2. Click **"New Project"**
3. Delete any existing code and paste the following:

```javascript
// FragIQ Beta Signup Form Handler
// Replace with your actual Sheet ID from Step 1
const SHEET_ID = 'YOUR_GOOGLE_SHEET_ID_HERE';

function doPost(e) {
  try {
    // Parse the incoming JSON data
    const data = JSON.parse(e.postData.contents);
    
    // Open the spreadsheet and get the first sheet
    const sheet = SpreadsheetApp.openById(SHEET_ID).getActiveSheet();
    
    // Append a new row with the form data
    sheet.appendRow([
      data.timestamp,
      data.email,
      data.deviceModel,
      data.androidVersion,
      data.experienceLevel,
      data.useCases,
      data.competitorApps,
      data.commitment14Days,
      data.commitmentFeedback,
      data.feedbackChannel,
      data.testingInterests
    ]);
    
    // Return success response
    return ContentService
      .createTextOutput(JSON.stringify({ status: 'success', message: 'Data saved successfully' }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    // Return error response
    return ContentService
      .createTextOutput(JSON.stringify({ status: 'error', message: error.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

// Test function to verify the sheet connection works
function testConnection() {
  try {
    const sheet = SpreadsheetApp.openById(SHEET_ID).getActiveSheet();
    Logger.log('Connection successful! Sheet name: ' + sheet.getName());
    Logger.log('Current row count: ' + sheet.getLastRow());
  } catch (error) {
    Logger.log('Error: ' + error.toString());
  }
}
```

4. **Replace `YOUR_GOOGLE_SHEET_ID_HERE`** with the Sheet ID you copied in Step 1

5. Click the **disk icon** or press `Ctrl+S` to save

6. Name the project "FragIQ Beta Form Handler"

---

## Step 3: Deploy as a Web App

1. Click **"Deploy"** → **"New deployment"**

2. Click the gear icon ⚙️ next to "Select type" and choose **"Web app"**

3. Configure the deployment:
   - **Description**: "FragIQ Beta Form v1"
   - **Execute as**: "Me (your email)"
   - **Who has access**: "Anyone"
   
   > ⚠️ "Anyone" is required for the form to work without authentication. The data is still only saved to YOUR private Google Sheet.

4. Click **"Deploy"**

5. **Authorize the app**:
   - Click "Authorize access"
   - Choose your Google account
   - Click "Advanced" → "Go to FragIQ Beta Form Handler (unsafe)"
   - Click "Allow"
   
   > This is safe - you're authorizing your own script to access your own sheet.

6. **Copy the Web App URL** - it looks like:
   ```
   https://script.google.com/macros/s/AKfycb...long-string.../exec
   ```

---

## Step 4: Update Your Website

1. Open `index.html`

2. Find this line near the bottom:
   ```javascript
   const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbwuD5dQ7QdSG59-z9au-2oQCbi5LH9WTLu-L4ek5NNRpIAQL5MLQheKfUda-r_0cg0RkQ/exec';
   ```

3. Replace `YOUR_GOOGLE_APPS_SCRIPT_URL_HERE` with your Web App URL from Step 3

4. Save and deploy your site

---

## Step 5: Test the Form

1. Open your website
2. Click "Join Beta on Google Play"
3. Fill out the form with test data
4. Submit
5. Check your Google Sheet - the data should appear!

---

## Troubleshooting

### Form submits but no data appears
- Verify the Sheet ID is correct
- Verify the Web App URL is correct
- Check the Apps Script execution log for errors

### "Authorization required" error
- Re-authorize the script (Deploy → Manage deployments → edit and redeploy)

### CORS errors in console
- The form uses `mode: 'no-cors'` which should handle this
- Ensure "Who has access" is set to "Anyone"

### To view submission logs:
1. In Apps Script, click **"Executions"** in the left sidebar
2. View recent executions and any errors

---

## Optional: Email Notifications

To receive an email when someone signs up, add this to your Apps Script:

```javascript
function doPost(e) {
  // ... existing code ...
  
  // After sheet.appendRow(), add:
  MailApp.sendEmail({
    to: 'your-email@gmail.com',
    subject: 'New FragIQ Beta Signup: ' + data.email,
    body: `New beta tester signup!\n\n` +
          `Email: ${data.email}\n` +
          `Device: ${data.deviceModel} (${data.androidVersion})\n` +
          `Experience: ${data.experienceLevel}\n` +
          `Use Cases: ${data.useCases}\n\n` +
          `View all signups: https://docs.google.com/spreadsheets/d/${SHEET_ID}/edit`
  });
  
  // ... rest of existing code ...
}
```

---

## Security Notes

- ✅ Form data is stored in YOUR private Google Sheet
- ✅ Only you can view the submitted data
- ✅ The Apps Script runs under your Google account
- ✅ No third-party services have access to the data
- ✅ HTTPS encryption in transit

---

## Updating the Form

If you need to update the deployed script:

1. Make your changes in Apps Script
2. Click **Deploy** → **Manage deployments**
3. Click the pencil icon ✏️ to edit
4. Change version to "New version"
5. Click **Deploy**

The URL stays the same, so no changes needed on your website.
