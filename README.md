# Land Distribution Machine

This repository contains a no-code-friendly system for:
1. Reading commercial land data from a public Google Sheet CSV.
2. Showing listings on a live Kansas City map and listing cards.
3. Publishing machine-readable JSON output and dynamic JSON-LD for SEO/AI crawlers.
4. Powering automation in Make.com or Zapier.

## What Is Included
- `index.html` - The full portal + map + cards + API mode + dynamic JSON-LD.
- `launch-assistant.html` - One-page setup wizard with checkboxes and one-click launch buttons.
- `AGENTS.md` - Architecture guardrails and 10-phase operating rules.
- `DEPLOYMENT_GUIDE.md` - Click-by-click GitHub Pages + Google Sheets setup.
- `AUTOMATION_BLUEPRINT.md` - Click-by-click Make.com and Zapier scenario builds.
- `SHEET_TEMPLATE.csv` - Ready-to-import sheet with clean headers only (no sample data).

## Required Google Sheet Columns
Your header row must include exactly:
1. `Property Name`
2. `Acreage`
3. `Zoning`
4. `Coordinates` (format: `lat,lng`)
5. `AI Summary`
6. `Owner Email`

## Daily Operator Flow (Simple)
1. Open your deployed portal page.
2. Paste your Google Sheet CSV URL into `Step 1`.
3. Click `Sync Listings Now`.
4. Use `Open JSON API` and `Download JSON` buttons as needed.

## Best Place To Start
Open `launch-assistant.html` first. It walks you through setup and launch in order.

## API Mode (for machines)
Add `?api=1&csv=YOUR_CSV_URL` to the portal URL.

Example:
`https://your-site.github.io/your-repo/?api=1&csv=https://docs.google.com/spreadsheets/d/e/.../pub?output=csv`

This returns a machine-readable JSON page with:
- Source URL
- Totals
- Valid listings array
