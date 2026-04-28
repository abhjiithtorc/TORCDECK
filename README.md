# Torc Decks

Strategy decks, proposals, and growth plans authored by Torc Infotech, hosted at `decks.torcinfotech.com`.

Built as static HTML using the Torc brand design system. Deployed via Vercel on every push to `main`.

---

## Live URLs

| Deck | URL | Status |
|------|-----|--------|
| Landing page | [decks.torcinfotech.com](https://decks.torcinfotech.com) | Live |
| Sharath Mascarenhas — Growth Plan v3 | [decks.torcinfotech.com/sharath](https://decks.torcinfotech.com/sharath) | Live |

---

## One-time setup (do this once)

### 1. Create the GitHub repo

```bash
# In an empty folder where you want the project to live
git init
git add .
git commit -m "Initial commit — Torc Decks"
git branch -M main

# Create repo on github.com/abhjiithtorc/torc-decks (public)
git remote add origin git@github.com:abhjiithtorc/torc-decks.git
git push -u origin main
```

### 2. Connect Vercel

1. Go to [vercel.com](https://vercel.com) and sign in with GitHub
2. Click **Add New → Project**
3. Import the `torc-decks` repo
4. Framework preset: **Other** (it's plain static HTML)
5. Click **Deploy** — first deploy takes ~30 seconds

You'll get a temporary URL like `torc-decks-abhijith.vercel.app`. The site is live.

### 3. Connect the custom domain

1. In Vercel project settings → **Domains** → add `decks.torcinfotech.com`
2. Vercel will give you a CNAME target (something like `cname.vercel-dns.com`)
3. In your DNS provider (wherever torcinfotech.com is registered):
   - Add a CNAME record: `decks` → `cname.vercel-dns.com`
4. Wait 5–60 minutes for DNS to propagate

After that, every push to `main` auto-deploys to `decks.torcinfotech.com`.

---

## Repository structure

```
torc-decks/
├── README.md                       # This file
├── vercel.json                     # Vercel deployment config
├── .gitignore
├── index.html                      # Landing page — deck directory
│
├── _shared/                        # Shared design system
│   ├── torc-deck-styles.css        # All Torc brand CSS
│   └── torc-deck-nav.js            # Keyboard + click navigation
│
└── sharath/                        # One folder per client
    └── index.html                  # The deck
```

---

## Adding a new deck

To add a new client deck (e.g. for OffshoreX):

1. Create a new folder: `mkdir offshorex`
2. Create `offshorex/index.html` — start by copying `sharath/index.html` as a template
3. Update the slide content (keep the structure, swap the data)
4. Add a row to `index.html` (the landing page) so it's listed
5. Commit and push:
   ```bash
   git add offshorex/ index.html
   git commit -m "Add OffshoreX growth plan deck"
   git push
   ```
6. Vercel deploys automatically. Live at `decks.torcinfotech.com/offshorex` in ~30 seconds.

---

## Conventions

- **Folder name = URL slug.** `sharath/` becomes `/sharath`. Keep it lowercase, no spaces.
- **The deck file is always `index.html`.** That's how the clean URL works.
- **All decks use the shared CSS and JS.** Don't inline styles — extend `_shared/torc-deck-styles.css` if you need new patterns, so all decks benefit.
- **Brand spec is in the skill, not in this repo.** See `claude.ai` skills → `torc-deck-design`. Don't deviate from the spec without updating it deliberately.
- **Decks are public.** Anyone with the URL can view. If a deck has sensitive numbers (rare — pricing is usually fine to share), use Vercel's password-protection feature in project settings.
- **Versions are part of the content, not the URL.** v3 of the Sharath deck lives at `/sharath`, not `/sharath/v3`. Old versions are accessible through Git history if needed.

---

## Brand system

The shared CSS in `_shared/torc-deck-styles.css` is the canonical implementation of the Torc deck brand spec.

Key constants:

- **Font**: Satoshi (loaded from Fontshare)
- **Primary blue**: `#1A2DD8`
- **Periwinkle (dark slides)**: `#6b7aff`
- **Ink (text)**: `#0a0a0a`
- **Off-white (cards)**: `#f5f5f7`
- **No rounded corners. No serifs. No italics for emphasis.**

If you change the shared CSS, every deck in the repo updates on next deploy. Useful for global tweaks, dangerous for accidental breakage. Test with the most complex deck before pushing.

---

## Local preview

To preview a deck locally before pushing:

```bash
# From the repo root
python3 -m http.server 8000
# or
npx serve .
```

Open `http://localhost:8000/sharath/` in your browser. Arrow keys to navigate.

---

## Contact

Built and maintained by **Abhijith Menon** — abhijith@torcinfotech.com
