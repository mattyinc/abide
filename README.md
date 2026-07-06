# Abide — Daily Discipline Builder

A tiny, single-file discipline tracker rooted in **John 15:4** — *"Abide in me, and I in you."*
Six two-minute daily reps, one per life domain (Spirit · Body · Mind · Money · Relationships · Craft),
anchored to routines you already have. Discipline as the fruit of abiding, not a willpower project.

## Run it

Open [`abide.html`](abide.html) — **double-click the file** or drag it into any browser.
No build step, no server, no backend, no network calls. Everything runs offline.

## What's inside

- **Today** — the six exercises as if-then intentions, an XP/level bar, and this week's verse.
- **Progress** — 30-day per-category completion, a full-day heatmap, level history, and badges.
- **Sabbath / Review** — one rest day a week (Sunday by default): no tasks, just a short reflection and weekly stats.
- **Settings** — edit every exercise, the verse rotation, grace-day count, and Sabbath day; export/import a JSON backup.

## Design principles

- **Tiny over ambitious** — every action is under two minutes (Fogg's B=MAP).
- **Anchored** — each exercise is an implementation intention: *after I…, then I…* (Gollwitzer).
- **No shame mechanics** — missed days never zero your XP or level. Two **grace days** per rolling 30 days
  cover a miss without breaking the streak (Lamentations 3:22-23 — *mercies new every morning*).
- **Calm, not a slot machine** — light theme by default with a manual dark toggle for evenings.

## Data & backup

All state lives in this browser's `localStorage` under a single key (`abide_app_state`).
Use **Settings → Export backup** to move between devices, and **Import backup** to restore.

## Design system

UI built from a [UI/UX Pro Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) design query —
warm cream, olive, and clay palette with Lora for the serif voice and Manrope for sans-serif UI, embedded as base64 so the
file stays fully offline and self-contained.

See [`discipline-app-spec.md`](discipline-app-spec.md) for the full build spec.
