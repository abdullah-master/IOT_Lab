# Aim
To integrate Google Cloud APIs for IoT applications, enabling data logging and analytics using Google Sheets and Drive.

# Google Cloud Integration for IoT

## Required APIs
- Google Drive API
- Google Sheets API

## Steps to Perform the Experiment

1. Visit the [Google Cloud Console](https://console.cloud.google.com/).
2. Create a new project named **IoT_Project**.
   ![image](https://github.com/user-attachments/assets/303dad42-47a4-482b-8645-22cfc209241d)
3. Select the newly created project (it may take a few seconds to appear).
4. Navigate to **API & Services**.
5. Click on **Enable APIs and Services**.
6. Search for **Google Drive API** and enable it.
   ![image](https://github.com/user-attachments/assets/09a3405f-b98b-4c50-83c2-648188561b36)
7. Similarly, enable the **Google Sheets API**.
    ![image](https://github.com/user-attachments/assets/6a3cf819-52e4-4c69-8b08-9c060156085c)
8. Go to **Credentials** -> **Create Credentials** -> **Service Account**.
    ![image](https://github.com/user-attachments/assets/4d4b1324-8737-41a3-be62-ff42c46b7378)
9. Assign the **Editor** role under **Basic**.
10. Click **Done** to finalize the service account creation.
11. Open the created Service Account email and navigate to **Keys**.
12. Under **Add Key**, select **Create New Key**.
    ![image](https://github.com/user-attachments/assets/78d945a1-c03e-4158-9a87-03fbfd6c3309)
13. Choose the **JSON** format and download the key file.
    ![image](https://github.com/user-attachments/assets/55ef112c-d068-4865-bbdd-64ef78e175a8)
14. Write and execute the provided Python code to interact with Google Sheets. Ensure you replace placeholders with actual values (e.g., sheet ID, credentials path).
15. Verify that the Google Sheet updates with the data.

### Python Code Example
```python
import gspread
import random
from oauth2client.service_account import ServiceAccountCredentials
from datetime import datetime
import time

# Define the scope and authenticate with Google
scope = ["https://spreadsheets.google.com/feeds", "https://www.googleapis.com/auth/drive"]
creds = ServiceAccountCredentials.from_json_keyfile_name('credentials.json', scope)
client = gspread.authorize(creds)

# Open the Google Spreadsheet by title or by key
spreadsheet = client.open("IoT_Data")  # or use .open_by_key("your_spreadsheet_key")

# Select the sheet to work with (e.g., the first sheet)
sheet = spreadsheet.sheet1

# Upload some data (example: adding rows to the sheet)
data = [
    ["Timestamp", "Temperature", "Humidity"],
    [str(datetime.now()), "25.3", "60"],
    [str(datetime.now()), "26.1", "58"],
]

# Update the sheet with the data
for row in data:
    sheet.append_row(row)

print("Data successfully uploaded to Google Sheets!")
```

