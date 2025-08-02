# Family Tree Client

This is a client to view a family tree stored in a Google Sheet. This repo currently hosts a client trying to fetch a family tree in a sheet, whose API key and account name are encrypted by the hash of a username and password.

## Usage
To view any other tree, link this client to your own Google account and sheet.

### Google Cloud Console Setup
1. Create a new project in [Google Cloud Console](https://console.cloud.google.com)
2. In the **APIs & Services** Section, click **Enable APIs and Services**, then find and enable the **Google Sheets API**
3. Create a **Service Account** by clicking **Create Credentials***
4. After creation go to the **Keys** tab and create a key in JSON format, then download.
5. Now, create a new Google Sheet, and share it with service account email as a viewer

### Sheet Data Structure
1. The opened sheet should be named **FamilyTree**
2. The format of a node or person in the sheet follows as such:
| Person | Spouse | Parent Index | 1 Image URI | 1 Image URI | 1 Image URI | 1 Image URI | 1 Image URI | 2 Image URI | 2 Image URI | 2 Image URI | 2 Image URI | 2 Image URI | 2 Image URI |
   
  | Cell  | Format |
| ------------- | ------------- |
| Person  | Name of Family Member  |
| Spouse  | Name of Spouse  |
| Parent Index  | (Parent Cell Row + 1), or (none)  |
| 1 Image URI  | Base64 Image Data URI - Member, or (none)  |
| 2 Image URI  | Base64 Image Data URI - Spouse, or (none)  |
   
   
