# CRSH Petition — Deploy to Vercel (Fresh Setup)

## What changed from before
- Removed `vercel.json` entirely. Vercel auto-detects a `public/` folder as static files and an `api/` folder as serverless functions — no manual config needed. This is the most reliable setup and avoids the 404 you were hitting.

## Files in this project
- `public/index.html` — the petition page
- `api/votes.js` — serverless function that reads/writes votes using Vercel KV
- `package.json` — declares the `@vercel/kv` dependency

## Fresh deploy steps (do this from scratch to avoid old cached config)

### 1. Delete the old Vercel project
- Go to your Vercel dashboard → open `crsh-petition-file` project → **Settings** → scroll to bottom → **Delete Project**
- This clears any stale build cache/config causing the 404.

### 2. Replace all files in your GitHub repo
- Go to your GitHub repo (`salim14300/crsh-petition`)
- Delete the old files: `vercel.json`, `public/index.html`, `api/votes.js`, `package.json`
- Upload the new versions from this folder, keeping the exact same structure:
  ```
  crsh-petition/
    ├── public/
    │     └── index.html
    ├── api/
    │     └── votes.js
    ├── package.json
    └── README.md
  ```
- **Important:** When uploading on GitHub's web UI, drag the `public` folder and `api` folder in as folders (not just the files inside them) so the nested structure is preserved. If GitHub flattens them, create the folders manually first (type `public/index.html` as the filename when creating a new file — GitHub auto-creates the folder).

### 3. Re-import the project on Vercel
- Go to https://vercel.com/new
- Import the `salim14300/crsh-petition` repo again
- Framework Preset: **Other**
- Leave Build Command, Output Directory, and Install Command **empty/default** — do not set an Output Directory manually
- Click **Deploy**

### 4. Add the KV database
- Once deployed, go to the project → **Storage** tab
- **Create Database** → **KV** → name it → **Connect** it to this project
- Vercel auto-adds the environment variables needed

### 5. Redeploy
- Deployments tab → latest deployment → "..." → **Redeploy**

### 6. Verify structure before you redeploy
Before redeploying, double check on GitHub that browsing to:
`github.com/salim14300/crsh-petition/blob/main/public/index.html`
actually shows the HTML file. If that URL 404s on GitHub itself, the file never uploaded correctly — fix that first, since Vercel can only deploy what's actually in the repo.

## Notes
- No login required to sign — just name + optional comment.
- All signatures are public to anyone with the link.
