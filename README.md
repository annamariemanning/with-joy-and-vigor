# With Joy & Vigor

Campaign site for **With Joy & Vigor — $30K for Pancreatic Cancer Research at Penn**.

Live site: **https://annamariemanning.github.io/with-joy-and-vigor/**

Everything you'd want to change during the campaign lives in **one file: `campaign.json`**. You never need to touch the HTML.

---

## How to update the site from your phone

You can do this entirely in a web browser (Safari/Chrome on your phone works fine).

### The amount raised updates itself — automatically 🎉

You do **not** need to edit the raised number by hand. A scheduled task (a "GitHub Action") checks your Penn campaign page — **givingpages.upenn.edu/30for30** — about every 30 minutes and copies the live total into the site for you. Every online gift is automatically reflected on the bar within roughly half an hour.

- **Want to refresh it right now** instead of waiting? On a computer, go to the repo → **Actions** tab → **Update donation total** → **Run workflow**. (There's also a "Run workflow" button in the GitHub mobile app under Actions.)
- **Leave the `"raised"` line alone.** The task overwrites it each run, so hand-edits won't stick.

### Counting checks or employer matches (gifts not made on the page)

Some gifts — mailed checks, employer matches — may not appear on the Penn page's online total. To include them, edit this one line in `campaign.json`:
```
"offlineGifts": 0,
```
Change `0` to the dollar total of those off-page gifts (numbers only). The task **adds** that to the Penn online total, so the bar shows everything. This line is yours — the task never overwrites it.

### Post an update to the "Updates" section

1. Same file, same pencil icon.
2. Find the `"updates"` list. Each update looks like this:
   ```
   { "date": "Aug 1", "text": "We're live. Day one, and you're already showing up — thank you." }
   ```
3. Add your new update **at the top of the list** (newest first), and make sure every line **except the last one** ends with a comma:
   ```
   "updates": [
     { "date": "Aug 5", "text": "Halfway to $15K after just five days. You people." },
     { "date": "Aug 1", "text": "We're live. Day one, and you're already showing up — thank you." }
   ]
   ```
4. Commit changes, same as above.

### Add the RSVP link when the party invite is ready (one-time)

The donate link is already set and live — every Donate button points to Penn's official giving page and opens in a new tab. You don't need to touch it.

When your Partiful invite exists, replace the `"#"` on the `rsvpUrl` line with the real link, keeping the quotes:

```
"rsvpUrl": "https://partiful.com/e/...",
```

Once it's set, the "RSVP on Partiful" button points to it automatically (and opens in a new tab). Until then, that button stays inert on purpose.

### The three rules that keep the file happy

- **Keep all the quotes and commas exactly as they are** — JSON is picky.
- `raised` and `goal` are plain numbers (no `$`, no commas).
- Every item in `updates` ends with a comma **except the last one**.

If you ever commit a typo and the file breaks, don't panic: **the site does not go down.** It quietly falls back to built-in default values until you fix the JSON. GitHub's editor will usually show a red mark where the mistake is.

---

## What's still placeholder (for a later session)

- `rsvpUrl` — Partiful link (in `campaign.json`)
- Party time — the `[TIME]` in `index.html`, "Come celebrate with us" section
- Bar name / neighborhood — the `[BAR NAME], [NEIGHBORHOOD]` in `index.html`, same section
- Contact email in the footer — the `[EMAIL — TBD]` in `index.html`
- `og-image.png` — the sharing-preview card; fine as is, but you can swap in a photo version later (keep the same 1200×630 filename and nothing else needs to change)

Everything else — the donate link, fund numbers, all copy — is final.

## Tech notes

Static site, no build step. `index.html` fetches `campaign.json` on load and renders the progress bar, countdown, links, and updates feed from it. If the JSON fails to load or is malformed, the page renders with fallback defaults baked into the HTML. Hosted on GitHub Pages from the `main` branch.
