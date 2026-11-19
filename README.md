# Volunteer Hub — permanent short links

Static redirect site (MIT). NFC stickers, attendee tickets and shared links point here, and `config.json` decides where they land
today. When the app moves to a new deployment, edit one line — no sticker ever needs rewriting.

| Link | Goes to |
|---|---|
| `https://<you>.github.io/vh/?b=042` | `<target>?b=042&src=nfc&sv=1&dv=<label>` (badge sticker) |
| `https://<you>.github.io/vh/?p=KEY` | `<target>?p=KEY` (a volunteer's personal page) |
| `https://<you>.github.io/vh/?c=CODE` | `<target>?c=CODE` (staff sign-in link) |
| `https://<you>.github.io/vh/?reg=community-day` | `<target>?reg=community-day` (an event's registration page) |
| `https://<you>.github.io/vh/?r=KEY` | `<target>?r=KEY` (a party's tickets) |
| `https://<you>.github.io/vh/?t=CODE` | `<target>?t=CODE` (one person's ticket — what the QR holds) |
| `https://<you>.github.io/vh/?go=training` | `links.training` from `config.json` |
| `https://<you>.github.io/vh/` | the app's home screen |

Any other parameters are passed through. Badge links get three extra parameters the app records in its
**Stickers** tab: `src=nfc` (opened from a sticker), `sv` (sticker format version) and `dv` (the `label` of the
config that served it — your "deployment version").

## Set up (5 minutes, free)

1. Create a GitHub repository named `vh` (short name = short links). Public is fine: it holds no data.
2. Upload `index.html`, `config.json`, `.nojekyll`, `LICENSE` and this README.
3. Settings → Pages → Build and deployment: **Deploy from a branch**, branch `main`, folder `/ (root)` → Save.
4. Your links start with `https://<your-username>.github.io/vh/`. Paste that into the app:
   **More → Stickers & links → Short-link base**.
5. Edit `config.json` → `target` = your Web app URL (ends in `/exec`) → Commit.

## Switch to a new deployment

Edit `config.json`: change `target`, bump `label` (e.g. `hub-v3.1`) and `updated` → Commit. Live within about a
minute. In the app, **Stickers & links → Check redirect** confirms the redirect points at that app.

## Optional

- **Named links** (`links`): unlimited — `"prep": "https://zoom.us/j/…"` makes `?go=prep` work.
- **Per-badge override** (`badgeOverrides`): `"042": "https://…/exec"` sends one badge somewhere else (e.g. a test
  deployment) without touching the others.
- **Custom domain**: add a `CNAME` file with e.g. `go.yourorg.org` and point that DNS name at GitHub Pages; links
  become `https://go.yourorg.org/?b=042`.
- Works on any static host (Cloudflare Pages, Netlify, your own server) — it's just two files.

## `config.json` fields

| Field | Meaning |
|---|---|
| `target` | Where links go: your Volunteer Hub Web app URL (`…/exec`). |
| `label` | Free text recorded with each sticker scan, e.g. `hub-v3`. Bump it when you switch deployments. |
| `stickerVersion` | Format version of the stickers you write (keep `1` unless the link format changes). |
| `updated` | Date you last changed this file (for your records). |
| `links` | Named short links for `?go=name` (lowercase names). |
| `badgeOverrides` | Badge number → URL, for exceptions. |
