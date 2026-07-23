# With Joy & Vigor

Campaign site for **With Joy & Vigor — $30K for Pancreatic Cancer Research at Penn**.

Live site: **https://annamariemanning.github.io/with-joy-and-vigor/**

Everything you'd want to change during the campaign lives in **one file: `campaign.json`**. You never need to touch the HTML.

---

## How to update the site from your phone

You can do this entirely in a web browser (Safari/Chrome on your phone works fine).

### Update the amount raised

1. Go to **github.com/annamariemanning/with-joy-and-vigor** and log in.
2. Tap the file **`campaign.json`**.
3. Tap the **pencil icon** (✏️, "Edit this file"). On a phone it may be hidden behind the **`⋯`** menu at the top right of the file.
4. Find the line that says:
   ```
   "raised": 8500,
   ```
   Change the number to the new total. **Numbers only — no dollar sign, no commas.** For example, if you've raised $12,340:
   ```
   "raised": 12340,
   ```
5. Scroll down and tap the green **"Commit changes"** button (you can leave the message it suggests).
6. Done. The live site updates itself in about a minute. Refresh the page to see the new bar.

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

### Add the real donate & RSVP links (one-time)

In the same file, replace the `"#"` with the real links, keeping the quotes:

```
"donateUrl": "https://giving.apps.upenn.edu/...",
"rsvpUrl": "https://partiful.com/e/...",
```

Once these are set, every Donate button and the RSVP button on the site point to them automatically.

### The three rules that keep the file happy

- **Keep all the quotes and commas exactly as they are** — JSON is picky.
- `raised` and `goal` are plain numbers (no `$`, no commas).
- Every item in `updates` ends with a comma **except the last one**.

If you ever commit a typo and the file breaks, don't panic: **the site does not go down.** It quietly falls back to built-in default values until you fix the JSON. GitHub's editor will usually show a red mark where the mistake is.

---

## What's still placeholder (for a later session)

- `donateUrl` — Penn giving page link (in `campaign.json`)
- `rsvpUrl` — Partiful link (in `campaign.json`)
- Bar name / time for the party (in `index.html`, "Come celebrate with us" section)
- Fund designation numbers (in `index.html`, "Ways to give" section)
- Photo of Dad (in `index.html`, the dashed photo frame)
- **[Sister's section]** story block (in `index.html`)
- Contact email in the footer (in `index.html`)
- `og-image.png` — currently a simple purple placeholder card; swap in a real 1200×630 photo card later (keep the same filename and nothing else needs to change)

## Tech notes

Static site, no build step. `index.html` fetches `campaign.json` on load and renders the progress bar, countdown, links, and updates feed from it. If the JSON fails to load or is malformed, the page renders with fallback defaults baked into the HTML. Hosted on GitHub Pages from the `main` branch.
