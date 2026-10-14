# Nexus: handoff for any AI coding assistant

## What it is
A personal iPhone-style web app (PWA) for Yash: job matching, priority Gmail with reply drafts,
goals with growth chart, shopping list with store links, order tracking, passcode lock.
Live at https://saxenayash062-ops.github.io/Nexus/ (GitHub repo `Nexus`, GitHub Pages, branch main).

## Files (repo root)
- index.html: the whole app (HTML, CSS, JS in one file, no build step, no frameworks)
- sw.js: service worker, network-first, same-origin only (never cache Gmail responses)
- manifest.json, icon-180.png, icon-512.png: Home Screen install

## How it works
- State object `S`, saved in the browser's localStorage under key `nexus2` (jobs, goals, orders, shop list, profile).
- Passcode hash in localStorage key `nexus_pin`.
- Gmail: Google Identity Services token client, scope gmail.readonly only. Token and mail stay in memory (`MAIL`), never saved.
- Job match score: `score(job)` compares keywords in the job description with `S.skills`.
- Tabs: Today, Jobs, Goals, Assistant, More. Each has a render function (today, jobs, goals, ast, more).
- Public OAuth Client ID is in index.html (`GCID`). It is not a secret. Test-user mode, owner's Gmail only.

## Privacy rules (must keep)
1. The repo is public. Never put phone, email, resume text, tokens, API keys or secrets in any file.
2. Personal data lives only on the phone (localStorage) or, later, in a private Supabase table with row-level security.
3. Gmail stays read-only. Never send mail's content to an AI service.
4. Any AI key must live in a server secret (Supabase Edge Function), never in index.html.

## Not built yet
- Real auto-apply on job portals (portals block bots; plan: tailor resume, user taps Approve, apply page opens)
- Live job-portal status tracking, push notifications, phone calls to support
- Synced private database (Supabase free tier) and an AI chat (Gemini free API behind an Edge Function)
- Ordering or price scraping for delivery apps (stores have no free public API; current version only opens each store's search)

## Rules for edits
Keep it one self-contained file, iOS look (system fonts, light/dark via CSS variables), free tools only, simple UI.
Test by opening index.html in a browser. After a commit, GitHub Pages updates in about 1 minute.

## Prompt to paste into the next AI
"You are maintaining the Nexus app in this repo. Read NEXUS_HANDOFF.md and index.html first.
Make the change I describe below, keep the privacy rules, keep everything free, and commit to main.
Change: <describe here>"
