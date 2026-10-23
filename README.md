# ProfileForge — README Studio & Template Marketplace

A responsive, local-first GitHub profile README builder. Built with plain HTML, CSS and JavaScript — no framework, build step, account, or required API key.

## Features

- **30 distinct template configurations** across six categories. Each template has its own heading treatment, category, color palette, description and Markdown structure.
- **Three creation paths:** use your own public GitHub profile, create a README for someone else using their public username, or enter details manually.
- **Public GitHub data:** fetches profile data and up to 100 public repositories using the GitHub REST API. No login/token is requested.
- **Repository selection:** filter repositories and choose which ones to include in the generated README.
- **Live Markdown preview/editor:** switch between a rendered preview and editable Markdown source. Manual edits are preserved until you change template or edit profile fields.
- **Quality checklist:** transparent content checks; not a hiring prediction.
- **Local drafts:** save multiple drafts in this browser, reopen/delete them, export a draft as JSON and import it on another device.
- **Export:** copy Markdown or download a `.md` file.
- **Responsive marketplace UI:** search, category filters, sorting, favorites and template selection.
- **No fake AI or publishing:** AI generation and direct GitHub publishing are not included. This static app does not send commits to GitHub.

## Run locally

1. Download and extract the ZIP.
2. Open the folder in VS Code.
3. Open `index.html` in a browser. Recommended: use the VS Code **Live Server** extension.
4. Internet access is needed for live GitHub API requests and optional Google Fonts. The manual builder and Markdown export can work offline after the files are available.

No `npm install` or build step is required.

## Deploy free

### GitHub Pages
1. Create a repository and upload `index.html`, `style.css`, `script.js`, and `README.md` to its root.
2. Open **Settings → Pages**.
3. Choose deploy from branch, select `main` and `/ (root)`, then save.
4. Open the URL GitHub Pages provides.

### Vercel (static)
1. Import the repository in Vercel.
2. Select framework preset **Other**.
3. Leave build command empty; set output directory to `.`.
4. Deploy.

The static site does not require server environment variables.

## GitHub API behavior and limits

The app calls:
- `GET https://api.github.com/users/{username}`
- `GET https://api.github.com/users/{username}/repos?type=owner&sort=updated&per_page=100`

Only public profile/repository information is used. The UI handles invalid usernames, missing profiles, API rate limits, and network failures. Unauthenticated GitHub API requests have a limited per-IP quota (commonly 60 requests/hour; GitHub may change limits and shared IPs can affect usage). This app fetches at most 100 repositories and does not paginate beyond that limit.

Language analytics count repositories by their primary language; this is not a lines-of-code calculation. A profile's public repository count can include repositories not present in the fetched first 100.

## Data and privacy

- Drafts and favorite template IDs are stored in the browser's `localStorage` on this device.
- No user account, analytics tracker, or server database is configured.
- Do not enter secrets, passwords, access tokens, private contact details, or sensitive information into a public README.
- A public email address will be visible to anyone who can read the README.
- GitHub usernames and public profile data are sent to `api.github.com` to fetch requested public information.
- The app uses `textContent`/HTML escaping for user-entered text in generated interface areas. Markdown preview is a deliberately limited renderer, not full GitHub Markdown parity. Links and images are limited to HTTP(S) URLs in the renderer.

## What's intentionally not included

- **AI bio generation:** not implemented in this static build. To add it, configure a provider and a server-side endpoint/serverless function. Keep provider keys in server-side environment variables, never in `script.js` or any browser-delivered file. AI provider use may cost money.
- **Direct GitHub publishing:** not implemented. Download the README, review it, then upload it to the profile repository yourself. Automated publishing requires GitHub OAuth/app authorization and a secure backend with appropriate permissions.
- **Private repository access:** not requested or supported.
- **Cloud-synced accounts / shared marketplace:** local drafts only. These need a backend and database.
- **Perfect GitHub rendering:** preview is approximate; verify the downloaded Markdown on GitHub before relying on it.

## GitHub profile README setup

For a profile README, create a public repository whose name exactly matches the GitHub username. Put the downloaded file at `README.md` in the repository root, then commit and push it.

## Troubleshooting

- **No profile loads:** check the username and internet connection; wait and retry if rate limited.
- **Preview looks different on GitHub:** GitHub has its own Markdown rules and strips/restricts some HTML/CSS. The downloaded Markdown is the source of truth; verify it on GitHub.
- **Clipboard is blocked:** use the Download README button.
- **Draft not saving:** browser storage may be disabled or full; export drafts as JSON regularly.
- **Fonts look different:** Google Fonts is optional; system fonts are used as fallback.


## Template design note

The 30 templates use separate Markdown structures, section ordering, headings, project presentation styles, and optional GitHub badges/stats—not just different colors. Pick a template, then switch between Preview and Markdown to inspect or edit its generated content. Editing the Markdown intentionally switches to a custom document so your edits are preserved until you choose another template. The in-app preview is a lightweight Markdown renderer, not a pixel-perfect replica of GitHub's renderer.
