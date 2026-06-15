# Attendee Matcher

A single-file, browser-based tool that matches **Zoom attendee reports** against a **main participant list** by email and phone number. Everything runs locally in the browser — no data leaves the machine, nothing is uploaded to a server.

## What it does

- Upload **one** main participant list (CSV) and **up to ~100** Zoom attendee report CSVs.
- For each person in the main list it tells you whether they **attended** or **did not attend**.
- It sums each attendee's **total join time** across every re-join session in every report.
- Phone numbers are cleaned (spaces, dashes, `+`, country code removed) and normalised to the **10-digit format used in Column G** of the main list.
- Matching is done by **email first, then phone** as a fallback.

## Output

On screen: four summary counts (in main list / attended / not attended / attendees not in main) plus a searchable, filterable table.

Downloads:
- **XLSX** with three sheets — `Summary`, `All Participants`, `Attendees Not In Main`.
- **CSV** of all participants.

Each participant row contains: Name, Email, Phone, Status (Attended / Not Attended), Total Duration (min), Sessions, Matched By.

## Expected file formats

**Main list** — a normal CSV with a header row. The tool auto-detects:
- an `email` column,
- a phone column (prefers one literally named `Phone`, i.e. Column G; falls back to `phoneNumber` / any phone column),
- a `name` column.

**Attendee report** — the standard Zoom webinar Attendee Report export. The tool skips the Host / Panelist blocks and reads the **Attendee Details** section automatically.

## Publish on GitHub Pages

1. Create a new repository and add `index.html` (and this `README.md`).
2. Go to **Settings → Pages**.
3. Set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`.
4. Save. Your tool will be live at `https://<username>.github.io/<repo>/`.

## Notes

- Large files are streamed, so 50–100 reports won't freeze the browser. Processing many big files can still take a little time.
- The on-screen table shows the first 400 matching rows; use search/filter to narrow, or download the full file.
- A person who attended both sessions (e.g. morning + evening) has their durations summed into one total.
