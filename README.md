# Google Sheets Data Sync (Demo)

Automates syncing columns from a **source** sheet to a **target** sheet by matching a shared **ID** column. Built with **Google Apps Script** (server-side JavaScript). This demo shows how to normalize identifiers, copy headers, batch read/write for performance, and avoid data drift in reporting workflows.

> **Use case:** Keep a reporting or “PIP/Target” tab updated with the latest fields from a “Sales/Source” tab by matching on a unique key.

---

## Features
- Match on a canonicalized ID (trim + non-breaking space cleanup).
- Copy a contiguous data range (e.g., B:O) to a different block in the target (e.g., AX:BK).
- Copy headers on first row so target columns stay labeled.
- Batch reads/writes (fast on large sheets).

---

## How It Works
1. Read **Source** sheet columns `A:O` (A = ID, B:O = payload).
2. Normalize IDs and build a map: `id -> [B..O values]`.
3. Ensure Target headers are set (row 1) in the destination block.
4. For each ID in **Target** column (default: AD), write mapped values into a destination range (default: AX:BK).

---

## Sheet Layout (Demo)
- **Source (tab name: `Sales`)**
  - `A`: `Source ID` (unique)
  - `B:O`: fields you want to mirror (14 columns)

- **Target (tab name: `Target`)**
  - `AD`: `Source ID` (IDs already present, row 2 down)
  - `AX:BK`: destination for mirrored fields (14 columns)

> You can rename tabs and change columns in the script constants.

---

## Setup
1. Open your Google Sheet.
2. **Extensions → Apps Script**.
3. Create a file `sync.gs` and paste the code from `/src/sync.gs`.
4. Adjust the constants if your tab names/columns differ.
5. Save and run `onOpen` once to add the **NASP Sync** custom menu.
6. From the sheet menu: **NASP Sync → Sync Sales → Target**.

---

## Demo Data
See `/sample/Sales.csv` and `/sample/Target.csv` for simple mock rows you can paste/import to test.

---

## Security / Notes
- This is a **demo**. Replace sheet/tab names safely; do not include proprietary names or data.
- Apps Script executes under your Google account; ensure you have access to both tabs.
- Consider adding: error logging to a “Logs” tab, dry-run mode, and column mapping validation.

---

## License
MIT (see `LICENSE`)
