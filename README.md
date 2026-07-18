# Sankalp

A private, single-page site for daily practice and daily identity. One file — `index.html` — with three views switched by the tabs at the top, no page reloads:

- **Today** — the day's arc: five sadhanas as a dawn-to-dusk ring, plus your leadership vow for any room you walk into.
- **Thoughts** — a running journal. No structure, no categories, just capture and timestamp.
- **Gallery** — YouTube links paired with the one idea each gave you.

Only three files total: `index.html`, `style.css`, `app.js`.

## How it works

Everything saves to **your browser's localStorage** first — instantly, as you type, no button needed. That's your safety net; nothing is ever lost mid-day.

**Sync to GitHub** is a separate, deliberate step. Click it once (end of day, ritual-style) and it:
1. Looks at what's new since your *last* sync — new thoughts, new gallery links, today's sadhana count.
2. Pushes one commit containing a full snapshot of all your data, with a commit message that summarizes just what's new (e.g. `Sankalp sync — 3 thoughts, 1 video, 4/5 sadhana — 18 Jul 2026`).
3. Your git log ends up as a clean, one-line-per-day record — a real trail of the practice, not a noisy commit per click.

This means:
- Entries are tied to the browser/device you use until you sync. If you use the site on your phone and laptop, sync from both and the *latest* sync wins as the source of truth in GitHub (the snapshot always overwrites the file — it doesn't merge across devices).
- Clearing your browser data before syncing will lose whatever hasn't been pushed. Sync regularly if this matters to you.
- Your GitHub personal access token is also stored in localStorage (see the setup section below) — treat it with the same care as your entries.

## Setting up GitHub sync

1. Create an empty GitHub repo (e.g. `sankalp`) if you don't have one.
2. On GitHub: **Settings → Developer settings → Fine-grained tokens → Generate new token.**
   - Repository access: only the one repo you made.
   - Permissions: **Contents → Read and write.** Nothing else.
3. In the site, click the ⚙ icon next to "Sync to GitHub" and enter your GitHub username, repo name, file path (defaults to `sankalp-data.json`), and the token.
4. Click **Save connection**, then **Sync to GitHub** whenever you want to commit the day's entries.

You can revoke the token from GitHub at any time, or hit **Disconnect** in the settings modal to remove it from this browser.

## Run it locally, right now

No build step. Just open `index.html` in a browser. Double-click the file, or:

```bash
open index.html        # macOS
start index.html       # Windows
```

## Host it for free on GitHub Pages

1. Create a new repo, e.g. `sankalp`.
2. Push these three files (`index.html`, `style.css`, `app.js`) to the repo root.
3. In the repo: **Settings → Pages → Source → Deploy from branch → main → / (root)**.
4. Your site is live at `https://<your-username>.github.io/sankalp/`.

Since this uses no backend, GitHub Pages is a perfect fit — it's just static files.

## Backing up your entries

Your data lives in the browser. To back it up, open the browser console on any page (F12 → Console) and run:

```js
copy(JSON.stringify({
  sadhana: localStorage.getItem('sankalp.sadhana.v1'),
  streak: localStorage.getItem('sankalp.streak.v1'),
  thoughts: localStorage.getItem('sankalp.thoughts.v1'),
  gallery: localStorage.getItem('sankalp.gallery.v1'),
}))
```

This copies a JSON snapshot to your clipboard — paste it into a text file and save it somewhere safe.

## Editing your leadership vow

The four vow statements live directly in `index.html` inside the `.vow-grid` block — plain HTML, easy to edit as your thinking evolves. This is meant to be a living document; change it as you change.

## What's next, if you want it

- Editable practice names (currently hardcoded in `app.js` → `PRACTICES`)
- Weekly/monthly view of your sadhana streak
- Export/import so entries sync across devices
- A "review" page that resurfaces old thoughts on their anniversary
