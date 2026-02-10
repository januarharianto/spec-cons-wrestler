# Special Considerations Wrestler

A client-side HTML tool that parses University of Sydney special considerations CSV exports and generates SEAMS2-compatible extension lists for upload.

## How to use

You can use this tool in two ways.

1. Download the project (Code → Download ZIP), unzip it and open index.html with any web browser. No internet connection is necessary.
2. Go to [januarharianto.github.io/spec-cons-wrestler](https://januarharianto.github.io/spec-cons-wrestler/). 

Then follow these steps.

1. Drag and drop your spec cons CSV file onto the page, or click the upload area to browse for it. This is the CSV export from ServiceNow, e.g. `x_uno57_student_ap_affected_assessments`.
2. Use the filter dropdowns to narrow down to a specific unit, semester, year, mode and location. The dropdowns only show valid combinations so you cannot select something that does not exist.
3. Pick an assessment from the list. Only assessments that have at least one extension will appear.
4. Check the preview table to make sure everything looks right.
5. Click **Download CSV** to save the file. The filename will look like `SEAMS2_{assessment}_{YYYYMMDD}.csv`.

## Output format

The downloaded CSV has four columns ready for SEAMS2 batch upload. once that is done, you can apply extensions to the new user groups on Canvas.

| Section Id | Section name | Student name | UniKey |
|------------|--------------|--------------|---------|
| (blank)    | Assessment Name - Mon-DD - Extension Type | (blank) | unikey  |

## Input CSV columns used

| Column | Purpose |
|---|---|
| `availability` | Parsed as `UNIT-SEMESTER-YEAR-MODE-LOCATION` for filtering |
| `state` | Only `Approved` rows are included |
| `assessment` | Assessment name, used for picking and for the output |
| `extension_in_calendar_days` | The extended due date in DD-MM-YYYY format. If this field has a value, the row is treated as an extension. |
| `u_outcome_type` | The type of extension, e.g. Simple Extension or Extension of time |
| `u_ticket_contact` | The student UniKey is extracted from the end of this field |

## Privacy and security

- No network requests are made. Fonts are system-native and a Content Security Policy blocks all external connections.
- All data exists only in browser memory. Nothing is stored in localStorage, cookies, or any persistent storage. Data is cleared on page refresh or when you click Reset.
- User data is rendered using safe DOM methods (`textContent`) so there is no risk of script injection from CSV content.

## License

MIT License. See source for full text.
