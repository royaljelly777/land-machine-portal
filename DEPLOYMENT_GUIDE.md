# Deployment Guide (No Terminal)

This guide uses only website buttons and menus.

## Part A: Prepare the Google Sheet
1. Open [Google Sheets](https://sheets.google.com) and create a sheet.
2. In row 1, add these exact headers:
   - `Property Name`
   - `Acreage`
   - `Zoning`
   - `Coordinates`
   - `AI Summary`
   - `Owner Email`
3. Add your property data in rows 2+.
4. Click `File` -> `Share` -> `Publish to web`.
5. In the dialog:
   - Choose the tab you want to publish.
   - Choose `Comma-separated values (.csv)` as format.
6. Click `Publish`.
7. Copy the generated URL (it should end with `output=csv`).
8. Paste that URL in a browser tab to confirm you can see raw CSV text.

## Part B: Create GitHub Repository
1. Open [GitHub](https://github.com) and sign in.
2. Click the `+` icon (top-right) -> `New repository`.
3. Enter a repository name (example: `kc-land-portal`).
4. Set visibility (`Public` recommended for crawler discovery).
5. Click `Create repository`.

## Part C: Upload Site Files (Web UI)
1. Open your new repo page.
2. Click `Add file` -> `Upload files`.
3. Drag and drop these files from your computer:
   - `index.html`
   - `launch-assistant.html`
   - `README.md`
   - `AGENTS.md`
   - `DEPLOYMENT_GUIDE.md`
   - `AUTOMATION_BLUEPRINT.md`
   - `SHEET_TEMPLATE.csv`
4. Scroll down.
5. In commit message, type: `Initial Land Distribution Machine portal`.
6. Click `Commit changes`.

## Part D: Turn On GitHub Pages
1. In your repository, click `Settings`.
2. In the left menu, click `Pages`.
3. Under `Build and deployment`:
   - Source: `Deploy from a branch`
   - Branch: `main`
   - Folder: `/ (root)`
4. Click `Save`.
5. Wait about 1-3 minutes.
6. Refresh the `Pages` section and open the published site URL.

## Part E: First Live Test
1. Open your published GitHub Pages URL.
2. In `Operator Mode`, paste your Google Sheet CSV URL.
3. Click `Sync Listings Now`.
4. Confirm:
   - Map markers appear.
   - Property cards appear.
   - `Valid Listings` metric is greater than zero.
   - `Open JSON API` works.
5. Share your live URL.

## Part F: Daily Operation (Simple)
1. Add or edit rows in Google Sheets.
2. Open your portal.
3. Click `Sync Listings Now`.
4. Use `Open JSON API` and `Download JSON` as needed.
