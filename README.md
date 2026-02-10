# Special Considerations Wrestler

A client-side HTML tool that parses University of Sydney special considerations CSV exports and generates SEAMS-compatible extension lists for upload.

## What it does

1. Upload a CSV export from ServiceNow (`x_uno57_student_ap_affected_assessments`)
2. Filter by **Unit**, **Semester**, **Year**, **Mode**, and **Location** — cascading dropdowns prevent invalid combinations
3. Select an assessment (only those with extensions are shown)
4. Preview and download a CSV formatted for SEAMS batch upload

### Output format

```
"Section Id","Section name","Student name","UniKey"
"","Assessment Name - Mon-DD - Extension Type","","unikey"
```

The output filename follows the pattern `SEAMS2_{assessment}_{YYYYMMDD}.csv`.

## How to use

Open `index.html` in any modern browser. No server, no install, no dependencies.

1. Drag and drop (or click to browse) your spec cons CSV
2. Use the filter dropdowns to narrow to a specific unit/semester/year
3. Select an assessment from the list
4. Review the preview table
5. Click **Download CSV** to save the SEAMS-compatible file

## Privacy and security

- **Fully offline** — no network requests are made. Fonts are system-native and a Content Security Policy blocks all external connections.
- **No data retention** — all data exists only in browser memory. Nothing is stored in localStorage, cookies, or any persistent storage. Data is cleared on page refresh or reset.
- **No XSS surface** — user data is rendered via `textContent` (DOM API), never `innerHTML`.

## Input CSV columns used

| Column | Purpose |
|---|---|
| `availability` | Parsed as `UNIT-SEMESTER-YEAR-MODE-LOCATION` for filtering |
| `state` | Only `Approved` rows are included |
| `assessment` | Assessment name, used for selection and output |
| `extension_in_calendar_days` | Extension due date (DD-MM-YYYY); presence indicates an extension |
| `u_outcome_type` | Extension type (e.g. Simple Extension, Extension of time) |
| `u_ticket_contact` | UniKey extracted from `"Name - unikey"` format |

## License

MIT License — see source for full text.
