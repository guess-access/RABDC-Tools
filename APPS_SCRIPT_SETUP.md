# Google Sheet write-back (row editor) — one-time setup

The Monthly Appointment table lets you edit any row (✏️ pencil → 💾 Save).
Saving to the Google Sheet needs a tiny web endpoint, because a website cannot
write to Google Sheets by itself. You only set this up once.

## 1. Open the sheet's Apps Script

Open the tracker sheet:
https://docs.google.com/spreadsheets/d/1WqqTaBpNh274tCFz3A3vkAMuFuQpxKgGww5q2S_4QnQ/edit

Menu → **Extensions → Apps Script**.

## 2. Paste this code

Delete anything that is there and paste:

```js
function doPost(e) {
  var body = JSON.parse(e.postData.contents);
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = body.tab ? ss.getSheetByName(body.tab) : ss.getSheets()[0];
  if (!sheet) return out({ ok: false, error: "Sheet tab not found: " + body.tab });

  var updated = 0;
  (body.cells || []).forEach(function (c) {
    if (c.row > 0 && c.col > 0) {
      sheet.getRange(c.row, c.col).setValue(String(c.value == null ? "" : c.value));
      updated++;
    }
  });
  return out({ ok: true, updated: updated });
}

function out(o) {
  return ContentService.createTextOutput(JSON.stringify(o))
    .setMimeType(ContentService.MimeType.JSON);
}
```

## 3. Deploy it

1. **Deploy → New deployment**
2. Click the ⚙ gear → choose **Web app**
3. **Description:** `tracker save`
4. **Execute as: Me**
5. **Who has access: Anyone**
6. **Deploy** → copy the **Web app URL**
   (`https://script.google.com/macros/s/AKf.../exec`)

> First time you will get an "unverified" warning because it is your own script:
> **Advanced → Go to … (unsafe)**. That is expected for a personal script.

## 4. Paste the URL into the tracker

In the site: **Dashboard → ⚙ Settings → Apps Script save URL (optional)** →
paste the `/exec` URL → **Save & Reload**.

## 5. Test

Click ✏️ on any row, change a cell, hit 💾. You should see
`✓ Saved to the Google Sheet — N cell(s) updated.` and the value updates in the sheet.

## Notes

- Without the URL the editor still works, but it says the change was only applied
  in the browser.
- The site sends the **row number** (from the header row it detected) and the
  **column position** of each changed cell, so the script writes to the exact cells.
- Keep the tab name in ⚙ Settings matching the tab you edit (default `APPT`).
- Anyone with the URL can post values, so treat it as a private link — do not
  publish it anywhere public.
