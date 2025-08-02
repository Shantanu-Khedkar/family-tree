# Family Tree Client

This is a client to view a family tree stored in a Google Sheet. This repo currently hosts a client trying to fetch a family tree in a sheet, whose API key and account name are encrypted by the hash of a username and password.

<img width="1080" height="720" alt="image" src="https://github.com/user-attachments/assets/2873193a-91a5-44e9-9a9c-722df47c0c0d" />


## Usage
To view any other tree, link this client to your own Google account and sheet.

### Google Cloud Console Setup
1. Create a new project in [Google Cloud Console](https://console.cloud.google.com)
2. In the **APIs & Services** Section, click **Enable APIs and Services**, then find and enable the **Google Sheets API**
3. Create a **Service Account** by clicking **Create Credentials**
4. After creation go to the **Keys** tab and create a key in JSON format, then download.
5. Now, create a new Google Sheet, and share it with service account email as a viewer

### Sheet Data Structure
1. The opened sheet should be named **FamilyTree**
2. The format of a node or person in the sheet follows as such:

| Person | Spouse | Parent Index | 1 Image URI | 1 Image URI | 1 Image URI | 1 Image URI | 1 Image URI | 2 Image URI | 2 Image URI | 2 Image URI | 2 Image URI | 2 Image URI | 2 Image URI |
|--------|--------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|--------------|

   
  | Cell  | Format |
| ------------- | ------------- |
| Person  | Name of Family Member  |
| Spouse  | Name of Spouse  |
| Parent Index  | (Parent Cell Row + 1), or (none)  |
| 1 Image URI  | Base64 Image Data URI - Member, or (none)  |
| 2 Image URI  | Base64 Image Data URI - Spouse, or (none)  |

3. To add childeren, simply continue adding rows with new people, and reference to parent indexes.
4. Make sure that all childeren point to the correct parent index.
5. Note that 'none' will cause clients to treat value as non-existent, while you may use 'Unknown' to label values not currently available, but which do exist.

### Client Setup
It is highly unlikely that anyone would ever want to use this client as it's codebase is a mess and hard to understand or update, but for documentation purposes, here is how to setup the client to interface with Google Sheets
1. In **index.html** find `SPREADSHEET_ID`, and replace with your spreadsheets's id (can be found in the url while sharing link), and make sure `SPREADSHEET_RANGE` matches your sheets's name at the bottom (not the same as file name).
2. You will need to generate new `CIPHERTEXT` variables in functions `validateP` and `validateU`
3. To do so, use **Crypto.html** in a browser with a JS console.
4. `getCiphertext(pass, data)` will allow you to make a ciphertext of `data` with `password`. You will need to put in the private key found in the JSON file downloaded while setting up Google Cloud Console
5. testCiphertext(ciphertext, pass) will allow you to test if decryption works with the ciphertext generated.
6. Both functions accept additional salt, iv arguments, which are set to random defaults. If using changed values, make sure they match the ones in the client.
7. Replace both instances of `CIPHERTEXT` with the ciphertext for the username and password (generate two ciphertexts using pass as first password then username...)
