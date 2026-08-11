# BACKSWING

A 12-week strength and mobility program, built as an installable web app. Designed for a former baseball player who now golfs: rotational power, hip and thoracic range, single-leg strength, and ongoing throwing-shoulder maintenance.

No accounts, no backend, no tracking. Everything you log stays in your own browser.

## What it does

- **12-week program** in three phases — Rebuild (wks 1–4), Build (wks 5–8), Express (wks 9–12), with deload weeks built in and a week-12 retest.
- **Set logging** — weight and reps per set, with estimated 1RMs and weekly tonnage computed automatically.
- **Rest timer** that starts itself when you check off a set, with an audible cue and haptics.
- **66-exercise library**, each with a coaching cue and a note on why it matters for the golf swing.
- **Five mobility routines**, including a six-minute pre-round warm-up.
- **Swap any exercise** for an alternative in the same category; home-gym substitutions listed throughout.
- **3, 4, or 5 days a week** — configurable in settings.
- **Works offline** via service worker. Add it to your Home Screen and it launches full screen like a native app.

## Stack

One `index.html` — no framework, no build step, no dependencies. Roughly 84 KB total. A service worker precaches the app so it runs with no signal; a `localStorage`-backed state layer holds your log, with clipboard and file backup as an escape hatch.

## Local development

Service workers and `localStorage` need an HTTP origin, so don't open the file directly — serve it:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

## Deploying

Connected to Cloudflare Pages. No build command, no build output directory — Pages serves the repo root as static files.

| Setting | Value |
| --- | --- |
| Framework preset | None |
| Build command | *(leave empty)* |
| Build output directory | `/` |

Every push to `main` redeploys automatically.

### After changing the app

Bump the `CACHE` constant in `sw.js` (e.g. `backswing-v1.0.1`) so installed phones pick up the new version instead of serving the cached one. The app shows an "Update ready" toast when a new service worker installs.

## Your data

Stored only in your browser, on your device. Settings → **Copy backup to clipboard** gives you a JSON blob to paste into Notes; **Restore from clipboard text** reads it back. Deleting the Home Screen icon or clearing Safari data wipes the log, so take a backup every few weeks.

## Disclaimer

Not medical advice. If something hurts sharply — especially a shoulder with throwing mileage on it — stop and get it looked at.
