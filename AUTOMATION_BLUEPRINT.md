# Automation Blueprint (Make.com + Zapier)

Goal: When a new row is added to Google Sheets, automatically:
1. Create a Google Doc listing sheet.
2. Copy the row into a public dataset tab (published CSV).
3. Publish a LinkedIn post.

Use either Make.com or Zapier. Both are documented below.

---

## Before You Build (One-Time)
1. In Google Sheets, create two tabs:
   - `Intake` (private working rows)
   - `PublicDataset` (public rows only)
2. Ensure both tabs have the same headers, including required fields:
   - `Property Name`, `Acreage`, `Zoning`, `Coordinates`, `AI Summary`, `Owner Email`
3. Add operational columns to `Intake`:
   - `Doc URL`
   - `LinkedIn URL`
   - `Automation Status`
   - `Published At`
4. In Google Docs, create one template document with placeholders:
   - `{{Property Name}}`
   - `{{Acreage}}`
   - `{{Zoning}}`
   - `{{Coordinates}}`
   - `{{AI Summary}}`
5. Publish only `PublicDataset` tab to web as CSV.

---

## Option A: Make.com Scenario (Module-by-Module)

### Scenario Name
`Land Machine - New Row Distributor`

### Module 1: Trigger
1. Click `Create a new scenario`.
2. Add module: `Google Sheets`.
3. Select trigger: `Watch New Rows`.
4. Connect Google account.
5. Set:
   - Spreadsheet: your workbook
   - Sheet: `Intake`
   - Limit: `1` (or higher if you batch process)
6. Click `Run once` to test and pull a sample row.

### Module 2: Validation Filter
1. Click the connection line after Module 1.
2. Add `Set up a filter`.
3. Name it `Required Fields Present`.
4. Add conditions:
   - `Property Name` is not empty
   - `Acreage` is not empty
   - `Zoning` is not empty
   - `Coordinates` is not empty
   - `AI Summary` is not empty
   - `Owner Email` is not empty

### Module 3: Google Doc Creation
1. Add module: `Google Docs`.
2. Choose action: `Create a Document from a Template`.
3. Select your template file.
4. Map template variables to row fields from Module 1.
5. Save the output `Document URL`.

### Module 4: Public Dataset Update
1. Add module: `Google Sheets`.
2. Choose action: `Add a Row`.
3. Spreadsheet: same workbook.
4. Sheet: `PublicDataset`.
5. Map all listing fields from Module 1.
6. Set `Published At` with current timestamp.

### Module 5: LinkedIn Post
1. Add module: `LinkedIn` (or `LinkedIn Pages`).
2. Choose one:
   - `Create a User Post` (personal profile), or
   - `Create a Company Update` (company page).
3. Build post text from mapped values:
   - Property Name
   - Acreage
   - Zoning
   - AI Summary
   - Optional source URL
4. Save returned post URL/ID.

### Module 6: Update Source Row Status
1. Add module: `Google Sheets`.
2. Choose action: `Update a Row`.
3. Target row: row number from Module 1.
4. Set:
   - `Doc URL` = URL from Module 3
   - `LinkedIn URL` = URL/ID from Module 5
   - `Automation Status` = `Published`
   - `Published At` = current timestamp

### Scheduling and Activation
1. Click `Scheduling`.
2. Set frequency:
   - For near real-time: every 15 minutes.
   - For daily batch: once daily at your preferred hour.
3. Click `Save`.
4. Toggle scenario `ON`.

---

## Option B: Zapier Zap (Step-by-Step)

### Zap Name
`Land Machine - New Row to Doc + Dataset + LinkedIn`

### Step 1: Trigger
1. Click `Create` -> `Zaps`.
2. Trigger app: `Google Sheets`.
3. Trigger event: `New Spreadsheet Row`.
4. Connect Google account.
5. Select Spreadsheet + Worksheet = `Intake`.
6. Click `Test trigger` and confirm sample row data appears.

### Step 2: Filter Required Fields
1. Add step: `Filter by Zapier`.
2. Rule group:
   - `Property Name` exists
   - `Acreage` exists
   - `Zoning` exists
   - `Coordinates` exists
   - `AI Summary` exists
   - `Owner Email` exists

### Step 3: Create Google Doc
1. Add action app: `Google Docs`.
2. Action event: `Create Document From Template`.
3. Select your template.
4. Map fields from Google Sheets trigger.
5. Test and capture output `Document URL`.

### Step 4: Append to Public Dataset Tab
1. Add action app: `Google Sheets`.
2. Action event: `Create Spreadsheet Row`.
3. Spreadsheet: same workbook.
4. Worksheet: `PublicDataset`.
5. Map required and optional listing fields.
6. Set `Published At` to Zap timestamp.

### Step 5: Publish to LinkedIn
1. Add action app: `LinkedIn`.
2. Action event (available by account type):
   - `Create Share Update`, or
   - `Create Company Update`.
3. Write post body using mapped fields.
4. Include a link to source listing or portal URL.
5. Test action and verify post appears in LinkedIn.

### Step 6: Update Intake Row Status
1. Add action app: `Google Sheets`.
2. Action event: `Update Spreadsheet Row`.
3. Use original row ID from trigger.
4. Set:
   - `Doc URL`
   - `LinkedIn URL`
   - `Automation Status` = `Published`
   - `Published At`

### Step 7: Turn Zap On
1. Click `Publish`.
2. Toggle Zap to `On`.
3. Add a test row in `Intake` and verify all downstream actions run.

---

## Recommended LinkedIn Post Template
Use this in Make/Zapier text mapping:

`New Kansas City Commercial Land Opportunity`

`Property: {{Property Name}}`
`Acreage: {{Acreage}}`
`Zoning: {{Zoning}}`
`Coordinates: {{Coordinates}}`

`Summary: {{AI Summary}}`

`Explore more listings: {{Portal URL}}`

---

## Daily "Trained Monkey" Checklist
1. Add new listing row to `Intake`.
2. Confirm required fields are filled.
3. Check automation run history (Make or Zapier) shows success.
4. Verify row status updated to `Published`.
5. Confirm row exists in `PublicDataset`.
6. Confirm LinkedIn post is live.
