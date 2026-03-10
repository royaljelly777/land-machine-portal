# AGENTS.md

## Project Name
Land Distribution Machine + Kansas City Commercial Land Discovery Portal

## Mission
Build a fully automated, 10-phase land data distribution system where Google Sheets is the single source of truth, and all outputs (portal, API, datasets, SEO schema, and social posts) are generated from structured sheet data.

## Non-Negotiable Rules
1. Work in strict sequence by phase.
2. Do not start the next phase without explicit user approval.
3. Prefer zero-install solutions: CDN scripts, static files, vanilla JavaScript, and no local build tools unless approved.
4. Provide non-technical, button-click deployment instructions for GitHub and Google Sheets when deployment is required.
5. Treat Google Sheets as the canonical database and preserve schema consistency across all downstream outputs.

## Required Data Schema (Strict Contract)
Every property record must include these fields:
1. `Property Name`
2. `Acreage`
3. `Zoning`
4. `Coordinates` (format: `lat,lng`)
5. `AI Summary`
6. `Owner Email`

### Recommended Extended Fields
- `Property ID`
- `Address`
- `City`
- `State`
- `ZIP`
- `Price`
- `Parcel Number`
- `Owner Email`
- `Source URL`
- `Image URL`
- `Listing Status`
- `Last Updated`

If required fields are missing, the record is invalid for publication.

## Canonical Field Handling Rules
1. Never rename required fields once in production.
2. If a new field is introduced, add it as optional first.
3. Use a stable header row in Google Sheets; downstream logic depends on exact header names.
4. Parse `Coordinates` into numeric latitude/longitude before map rendering and schema output.
5. Keep `AI Summary` concise, factual, and safe for public web display.

## 10-Phase Architecture

### Phase 1: Guardrails and Governance
- Create and maintain this `AGENTS.md`.
- Define schema, phase gates, SOPs, and quality controls.
- Outcome: execution framework approved.

### Phase 2: Core Portal + API Engine
- Build `index.html` as a single-page app.
- Fetch Google Sheet public CSV dynamically.
- Render Leaflet map markers and property cards.
- Generate dynamic JSON-LD `RealEstateListing` schema from live data.
- Outcome: public portal and machine-readable SEO layer live.

### Phase 3: Automation Blueprint
- Design Make.com or Zapier workflows triggered by new Google Sheet rows.
- Automate document generation, dataset refresh, and social publishing pipeline.
- Outcome: repeatable click-path automation design.

### Phase 4: Data Normalization Layer
- Validate row structure and required fields.
- Normalize units (acreage), coordinates, and status values.
- Reject or quarantine malformed records.
- Outcome: clean, reliable data enters distribution.

### Phase 5: Programmatic SEO Expansion
- Create location and zoning-focused landing templates.
- Attach listing-level and collection-level JSON-LD.
- Generate crawl-friendly internal links and canonical paths.
- Outcome: search index coverage and semantic clarity increase.

### Phase 6: Public Dataset Syndication
- Publish updated CSV/JSON snapshots to public endpoints.
- Ensure consistent column ordering and metadata notes.
- Outcome: reusable public dataset for humans and bots.

### Phase 7: API Hardening and Query Layer
- Provide filterable, documented API output from sheet data.
- Add predictable query parameters (city, zoning, acreage range, status).
- Outcome: stable integration surface for third-party consumers.

### Phase 8: Social Distribution Engine
- Auto-generate social post copy from new/updated properties.
- Syndicate to LinkedIn (and optional additional channels).
- Outcome: continuous distribution loop from sheet updates.

### Phase 9: Monitoring and Resilience
- Add health checks for CSV availability, map render status, and schema generation.
- Add fallback UX for data fetch failures.
- Outcome: operational reliability and fast incident detection.

### Phase 10: Optimization and Scale
- Track SEO indexation, impressions, clicks, and conversion actions.
- Tune schema richness, page structure, and automation cadence.
- Outcome: sustained growth and machine scalability.

## Standard Operating Procedures (SOP)

### SOP-1: Before Any Build Step
1. Confirm current phase.
2. Confirm that previous phase is explicitly approved.
3. Confirm data schema fields are unchanged or properly versioned.

### SOP-2: During Development
1. Keep implementation static-host friendly for GitHub Pages.
2. Use CDN dependencies only (Tailwind CDN, Leaflet CDN).
3. Avoid server-side requirements unless user explicitly requests and approves.

### SOP-3: Data Intake from Google Sheets
1. Use published CSV URL only.
2. Parse header row dynamically, then map to canonical names.
3. Validate required fields and skip invalid rows with clear warnings.

### SOP-4: SEO/AI Readiness
1. Generate JSON-LD dynamically from live dataset.
2. Ensure each valid property can become a structured listing object.
3. Keep schema in sync with visible page content.

### SOP-5: Deployment Guidance
1. Provide exact click-by-click instructions for GitHub and Google Sheets UIs.
2. Avoid terminal-heavy deployment instructions for non-technical users.
3. Include rollback instructions when relevant.

## Quality Gates (Must Pass)
1. Schema Integrity: all required fields present per valid record.
2. Render Integrity: cards and map markers align with same source row.
3. SEO Integrity: JSON-LD is valid and representative of visible listings.
4. Automation Integrity: trigger and action modules map to correct sheet columns.
5. UX Integrity: clear empty/error states for missing or invalid data.

## Error Handling Policy
1. Never silently fail data parsing.
2. Log row-level validation issues for debugging.
3. If data source is unavailable, show a user-facing status message and preserve page shell.

## Change Management
1. Any breaking schema change requires a documented migration note.
2. Keep a changelog section in this file for major architecture updates.
3. Do not remove required fields from the contract.

## Security and Privacy Baseline
1. Publish only intended public data.
2. Do not expose private owner contact details unless explicitly approved for public release.
3. Sanitize text outputs before injecting into HTML.

## Changelog
- 2026-03-04: Initial project guardrails created with 10-phase architecture, schema contract, SOPs, and quality gates.
