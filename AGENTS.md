# Repository Guidelines

## Project Structure & Module Organization
- Root contains `index.html` (single‑page app) and `README.md`.
- If adding files, prefer: `scripts/` for JS, `styles/` for CSS, `assets/` for images/data. Keep DOM IDs stable (e.g., `clientId`, `sheetId`, `btnRead`, `btnAppend`, `out`).
- Purpose: track disc golf putting sessions by reading/appending rows in a Google Sheet.

## Build, Test, and Development Commands
- Run locally (no build step): `python3 -m http.server 5173` → open `http://localhost:5173`.
- Alternative servers: `npx serve .` or `npx http-server -p 5173`.
- Deploy: push to `main` and enable GitHub Pages (root). Pages serves `index.html`.

## Coding Style & Naming Conventions
- Stack: vanilla JS + HTML/CSS. Indentation: 2 spaces. Quotes: double ("…").
- JS naming: `camelCase` for variables/functions; event handlers `on…`; button IDs prefixed `btn…`.
- Filenames: lowercase with hyphens if added (e.g., `putting-stats.js`). Keep functions small and DOM‑driven.

## Testing Guidelines
- Manual flow: sign in, read `Sheet1!A1:C10`, append a row, confirm it appears in the sheet.
- Use a throwaway test sheet. Validate errors (popup blocked, origin mismatch, insufficientPermissions) per `README.md`.
- Optional automation: Playwright to assert DOM state and stub `fetch` for Sheets API calls.

## Commit & Pull Request Guidelines
- Commits: imperative mood, concise scope. Recommended prefixes: `feat:`, `fix:`, `docs:`, `chore:`.
- PRs: describe the change, include before/after screenshots if UI changes, link issues (if any), and note the sheet/range used for testing.

## Security & Configuration Tips
- Do not commit real OAuth `CLIENT_ID` or sensitive spreadsheet IDs. Keep credentials user‑entered or local‑only in `index.html` during testing.
- Ensure OAuth origin matches your Pages URL exactly (no trailing slash). Tokens are short‑lived and held in memory only.

## Architecture Overview
- Single static page uses Google Identity Services to obtain an access token and calls the Sheets API to read/append putting data. Extend inline or extract logic to `scripts/putts.js` as the app grows.

