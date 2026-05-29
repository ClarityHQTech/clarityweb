# ClarityHQ · Brand Context Protocol — Demo

Static HTML demo of ClarityHQ's BCP integration inside Slack. Two synchronized views — desktop and mobile — sharing the same flow, brand voice check beats, and agentic engine log.

## Routes

| URL | Serves |
|-----|--------|
| `/` | Landing page with auto-detect (mobile devices auto-redirect to `/mobile` after a beat) |
| `/?stay` | Landing page without auto-redirect (manual choice) |
| `/desktop` | Desktop video demo (1140px Slack layout) |
| `/mobile` | Mobile video demo (Slack mobile chrome, phone-tuned) |

## Deploy to Vercel

### Option A — Drag & drop (fastest)

1. Go to https://vercel.com/new
2. Drag this entire `clarity-bcp-demo` folder onto the page
3. Click **Deploy**
4. Done — Vercel gives you a `https://clarity-bcp-demo-xxx.vercel.app` URL

### Option B — Vercel CLI

```bash
npm i -g vercel
cd clarity-bcp-demo
vercel
# follow the prompts; accept defaults
```

For production deploy:
```bash
vercel --prod
```

### Option C — GitHub + Vercel (recommended for ongoing updates)

1. `git init && git add . && git commit -m "Initial"` in this folder
2. Push to a new GitHub repo
3. On https://vercel.com/new, import that repo
4. Framework preset: **Other** (it's static HTML)
5. Build command: (leave empty)
6. Output directory: (leave empty — Vercel detects)
7. Deploy

Every push to `main` redeploys automatically.

## Custom domain (optional)

Once deployed, in the Vercel project → **Settings** → **Domains**, add your custom domain (e.g. `demo.clarityhq.ai`) and follow the DNS instructions.

## Local preview

```bash
# Python
python3 -m http.server 8000

# Or with npx
npx serve .
```

Then open `http://localhost:8000` (Python) or `http://localhost:3000` (serve).

> Note: opening `index.html` directly via `file://` will work, but the clean-URL routing (`/desktop`, `/mobile`) only works behind a server. Local: use one of the commands above. Production: Vercel handles it via `vercel.json`.

## Files

```
clarity-bcp-demo/
├── index.html        Landing + auto-detect router
├── desktop.html      Desktop video demo
├── mobile.html       Mobile video demo
├── vercel.json       Vercel config (cleanUrls + security headers)
└── README.md         This file
```

## What's inside the demos

Both demos auto-play a 33-beat scripted flow through:

1. Greeting → choose between new layer / existing
2. Brand asset ingestion → ICP card
3. Brand Book card (Sage archetype, voice, palette)
4. Brand Context Protocol (BCP) endpoint exposed
5. **Brand Voice Check hero beat** — off-brand draft (`"fully automated… 50% off, today only"`) flagged 31/100 against the real ClarityHQ BCP rules, then rewritten to PASS at 94/100
6. Campaign hypotheses → built campaign
7. Browse brands → Ceremony client
8. Generate posts (3 variants) → approve → schedule
9. Route to Growth Lead

The Agentic Engine panel below Slack streams which agent fires per turn (ICP / Brand / BCP / Campaign / Creative / Outreach) and which tools light up (Apify, Serper, Nano Banana, BCP, Claude Code, HubSpot, Smartlead, WhatsApp).

Transport controls (play / pause / next / prev / restart) sit in the top rail on desktop and just below the channel header on mobile.

## Notes

- These are scripted **video** demos — they don't call any external APIs. Safe to share publicly.
- Interactive (live AI) variants exist separately — those call the Claude API and only work inside Claude.ai's environment.
- BCP brand data shown is real: pulled from `https://www.brandcontextprotocol.com/brands/clarityhq/brand-context.json`.
