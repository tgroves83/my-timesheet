# my-timesheet

Web Form to Google Sheets Application
This project is a simple web application that allows users to submit data via a web form. The submitted data is then sent to a Google Sheets document using a Google Apps Script as the backend.

Features
A clean and responsive form built with HTML and CSS.
Data is submitted to Google Sheets using JavaScript and Google Apps Script.
The application is easy to deploy and configure.
Prerequisites
Basic knowledge of HTML, CSS, and JavaScript.
A Google account to access Google Sheets and Google Apps Script.
Google Chrome or Microsoft Edge browser for development and testing.
Getting Started
Step 1: Setting Up Google Sheets and Google Apps Script
Create a Google Sheet:

Open Google Sheets and create a new spreadsheet.
Set up the headers in the first row (e.g., Name, Email, Message).
Create a Google Apps Script:

Open the Google Sheet and navigate to Extensions > Apps Script.
Replace the default code with your Code.gs script (see below).
javascript
Copy code
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = e.parameter;

  var fechaCell = sheet.getRange("C2"); // Example cell, change to fit your sheet
  var pDpCell = sheet.getRange("F2");
  var alCell = sheet.getRange("H3");

  fechaCell.setValue(data.Column_3);
  pDpCell.setValue(data.Column_6);
  alCell.setValue(data.Column_8);

  return ContentService.createTextOutput('Success');
}

function doGet(e) {
  return ContentService.createTextOutput("This web app is intended for form submissions only.");
}
Deploy the Script:
Click on Deploy > Manage Deployments.
Create a new deployment, set it as a Web App.
Choose access permissions (e.g., "Anyone with the link").
Copy the Web App URL for later use.
Step 2: Setting Up the Web Form
Create an HTML file (index.html):
Add the form code (see below) to your HTML file.
html
Copy code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta charset="utf-8">
    <title>Timesheet</title>
    <style>
        /* Add your styles here */
    </style>
</head>
<body>
    <div class="form-container">
        <h1>Timesheet</h1>
        <form id="submissionForm">
            <div class="form-group">
                <label for="Column_6">Periodo del pago</label>
                <input type="text" id="Column_6" name="Column_6" required>
            </div>
            <div class="form-group">
                <label for="Column_3">Fecha</label>
                <input type="text" id="Column_3" name="Column_3" required>
            </div>
            <div class="form-group">
                <label for="Column_8">Al</label>
                <input type="text" id="Column_8" name="Column_8" required>
            </div>
            <div class="form-group">
                <button type="submit">Submit</button>
            </div>
        </form>
        <div id="result"></div>
    </div>
    <script>
        document.getElementById('submissionForm').addEventListener('submit', function(e) {
            e.preventDefault();
            var formData = new FormData(this);
            var xhr = new XMLHttpRequest();
            xhr.open('POST', 'YOUR_WEB_APP_URL_HERE', true);
            xhr.onload = function() {
                if (xhr.status === 200) {
                    document.getElementById('result').innerText = 'Submission successful!';
                } else {
                    document.getElementById('result').innerText = 'An error occurred. Please try again.';
                }
            };
            xhr.send(formData);
        });
    </script>
</body>
</html>
Replace the YOUR_WEB_APP_URL_HERE with your Google Apps Script web app URL that you copied earlier.
Step 3: Running the Application
Deploy Locally:

You can run the HTML file directly by opening it in a browser or hosting it using GitHub Pages, or a local server.
Testing:

Enter data into the form and click "Submit".
Check the connected Google Sheet to ensure the data has been correctly added.
Troubleshooting
No Data in Google Sheets:
Ensure the Web App URL is correct.
Check the Google Apps Script execution log for errors.
CORS Issues:
Run the HTML file via a local server or ensure proper deployment.
Security Errors:
Make sure your browser allows access to the URL by disabling tracking prevention or security settings temporarily.
Contributing
If you'd like to contribute, please fork the repository and submit a pull request. Contributions, bug reports, and feature requests are welcome!