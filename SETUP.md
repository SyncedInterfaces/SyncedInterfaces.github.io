# Setting Up Your Site (Synced Interfaces)

The site lives in `Site/` and updates itself from `Discord.lua` every time you run `python deploy.py`.
This is the one-time setup to put it online.

## 1. Create the GitHub repo

- Go to https://github.com/new
- Repo name **must be exactly**: `yourusername.github.io` (replace `yourusername` with your actual GitHub username)
- Set it to **Public**, click Create

## 2. Connect the Site folder to GitHub

Open PowerShell and run these one at a time (replace `<you>` with your GitHub username in the last command):

```powershell
cd "c:\Users\sync\Downloads\Files\Resources\Roblox\Scripts\Site"
git init -b main
git add -A
git commit -m "site"
git remote add origin https://github.com/<you>/<you>.github.io.git
git push -u origin main
```

- A browser window will pop up asking you to sign in to GitHub — do that once, you won't be asked again.
- After the push finishes, wait ~1 minute and open `https://<you>.github.io` — your site is live.

## 3. Fill in the config

Edit `Site/site_config.json`:

```json
{
    "name": "Synced Interfaces",
    "tagline": "A Roblox utility script with full alt control.",
    "repoUrl": "https://github.com/<you>/<you>.github.io",
    "scriptUrl": "",
    "accent": "#e2564b",
    "webhooks": {
        "changelog": "https://discord.com/api/webhooks/xxxx/yyyy"
    }
}
```

- `scriptUrl` — optional, link to your loader/raw script. Leave `""` for now if you don't have one.
- `webhooks.changelog` — Discord → your changelogs channel → Edit channel → Integrations → New Webhook → copy URL and paste it here.

## 4. That's it — from now on just deploy normally

Every time you run:

```powershell
python deploy.py
```

it automatically:
- rebuilds the website pages from `Discord.lua` (the CHANGELOG/FEATURES tables)
- commits + pushes the update to your site (if step 2 was done)
- posts the newest changelog entry to your Discord webhook (if step 3 was done)

You never touch the site manually. To change what shows on it, edit the tables in `Modules/UI/Discord.lua` like normal.

## Optional flags

| Command | What it does |
|---|---|
| `python build_site.py` | Rebuild the pages only, no push/no webhook |
| `python deploy.py --no-site` | Deploy but skip the site step entirely |
