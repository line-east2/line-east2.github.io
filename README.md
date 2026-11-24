# Line East2 Open JC Analysis

Daily Open Job Card (JC) portal for the East2 region.

- **Admin** uploads the daily Open JC raw file, sees the dashboard (CCM, segment, dealer and division wise; binning and age analysis) and downloads the latest data in Excel.
- **CCMs** open the update page with the team access code, pick their name, filter by segment / dealer / division and fill **Binning**, **Sub Binning** and **CCM remark** for each open JC, then press **Save**.

**This repository holds code only. No JC data is stored here.** All data sits in a private Google Sheet in the admin's Google Drive, written by the Apps Script back-end.

| Part | Where | What |
|---|---|---|
| `index.html` | GitHub Pages | The portal (CCM page and `?page=admin`) |
| `config.js` | GitHub Pages | Back-end address and portal title |
| `Code.gs` | Google Apps Script (not in this repo) | Private back-end |

## Links
- CCM update page: https://line-east2.github.io/
- Admin: https://line-east2.github.io/?page=admin

## How it works
- **Daily upload** (admin): the sheet that has the `JC #` and `Division` headers is read. CCM updates already saved are carried forward by JC #. JCs missing from the new file are moved to a *Closed* sheet (kept 60 days). If `CCM` is blank or `UNMAPPED`, the CCM last seen for that division is used. If `Segment` is blank, a division code starting with 3 is PV, otherwise EV.
- **Binning list**: if the uploaded workbook also has the binning list sheet (bin names in row 1, sub-bins below), the dropdowns are updated from it. Bins named HV / EV / E_Drive are shown for EV JCs only.
- **Saving** (CCM): changes are kept in the browser as they are typed. Save sends them in batches of 25. If the network drops, the unsent ones stay on the device and are sent automatically when the network returns or the page is opened again.
- **Ageing buckets**: 0-2, 3-7, 8-15, 16-30, 31-60, >60 days (from `JC Open Days`).

## Updating the back-end code
Apps Script → **Deploy → Manage deployments → Edit → Version: New version → Deploy**. The URL stays the same.
