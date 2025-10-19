# Sheets-as-DB (GitHub Pages Starter)

This is a zero-backend starter that reads/writes Google Sheets from a **static** web app using Google Identity Services (GIS) + the Sheets API.

## 1) Create OAuth Client ID
1. Go to https://console.cloud.google.com/ → create a project.
2. Enable **Google Sheets API**.
3. Configure **OAuth consent screen** (External is fine for testing). Add the scope:
   - `https://www.googleapis.com/auth/spreadsheets`
4. Create **OAuth 2.0 Client ID** → type **Web application**.
5. Add your GitHub Pages origin to **Authorized JavaScript origins** (no trailing slash):
   - `https://<username>.github.io` (user site), and/or
   - `https://<username>.github.io/<repo>` (project site, optional)
   - include your custom domain if you have one

> You do **not** need an Authorized redirect URI for the GIS token popup flow.

## 2) Deploy to GitHub Pages
- **Option A (User site)**: name the repo `<username>.github.io`.
  - Push this folder's contents to the repo `main` branch.
  - Visit `https://<username>.github.io` once Pages builds.
- **Option B (Project site)**: use any repo name.
  - In **Settings → Pages**, set **Source** to `Deploy from a branch`, choose `main` and `/ (root)` (or `/docs` if you put files there)`.
  - Visit `https://<username>.github.io/<repo>`.

## 3) Try it
1. Open your Pages URL.
2. Paste your **OAuth CLIENT_ID** (ends with `.apps.googleusercontent.com`) into the page.
3. Paste a **Spreadsheet ID** that you can access (you can find it in the Sheet URL).
4. Click **Sign in with Google**, then **Read** or **Append**.

## Notes
- This demo writes a timestamp + event + random value into `Sheet1!A:C`.
- If you want a fixed CLIENT_ID, hardcode it in `index.html` instead of typing it each time.
- For SPA routers (e.g., React), add a `404.html` that redirects to `index.html` to handle deep links on GitHub Pages.
- Avoid shipping secrets (service-account keys) in a static site.

## Troubleshooting
- **popup_blocked_by_browser**: the token popup must be user-initiated (click the button).
- **origin_mismatch**: ensure your Pages URL is in **Authorized JavaScript origins**.
- **insufficientPermissions**: you didn’t request the Sheets scope or you edited it after token mint—re-auth.
- **404 on /values**: check the Spreadsheet ID and that the sheet/tab name exists (default `Sheet1`).

Happy hacking!
