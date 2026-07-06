# Project: "Abide" — Daily Discipline Builder
### Assignment brief for Claude Code (Fable) — build phase not started, spec only

---

## 1. Purpose

Matty has a pattern: strong starts, weak follow-through, across health, finances, and career goals. This is not a motivation problem — behavior science (Fogg's B=MAP model, Gollwitzer's implementation-intention research) shows follow-through fails from poor *design*, not weak character. The fix is small daily reps, anchored to existing routines, tracked visibly, with immediate reward.

Theologically: discipline is the *fruit* of abiding in Christ (John 15:5 — "apart from me you can do nothing"), not a willpower project run in parallel to faith. The app should build the discipline **muscle** first, over roughly 6 months (now → end of year), through tiny daily exercises — before any bigger app (budget tool, fitness tracker, etc.) gets built. This *is* the app. It is not a placeholder for a future app — it is the actual deliverable.

---

## 2. Core design principles (non-negotiable)

1. **Tiny over ambitious.** Every daily exercise must be completable in under 2 minutes. (Fogg: ability beats motivation — shrink the behavior, not the person.)
2. **Anchored, not floating.** Every exercise is framed as an if-then / after-this implementation intention (Gollwitzer), e.g. "After I pour my morning coffee, then I open this app."
3. **Immediate celebration.** Every completed action gets instant visual/audio-free feedback (no sound required, this is used at work sometimes) — a checkmark animation, a small XP tick, a Scripture line.
4. **No shame mechanics.** Missed days do not reset everything to zero (see streak-forgiveness logic in §5). Guilt-based UX is explicitly against the point of this — Christ does not run a shame-based discipline system, and neither should this.
5. **Categories mirror his real life**, matching his existing `metamorphosis_2026.html` domains: **Spirit, Body, Mind, Money, Relationships, Craft.**
6. **Single-file HTML app.** Vanilla JS, no frameworks, no build step, no backend. Dark theme, clean typography (matches his established personal-project pattern). Data persists in `localStorage`. Must run by double-clicking the file or opening in any browser — no server required.

---

## 3. Scripture grounding (build into the UI, not bolted on)

- App name: **Abide** (John 15:4 — "Abide in me, and I in you")
- Splash/home screen verse, rotating weekly, minimum starter set:
  - John 15:5 — apart from Him, nothing
  - Galatians 5:22-23 — self-control as fruit of the Spirit, not raw effort
  - 1 Corinthians 9:24-27 — running to win the prize, disciplined training
  - Hebrews 12:1 — running with endurance, eyes on Jesus
  - Philippians 4:13 — strength through Christ
  - Proverbs 16:3 — commit your work to the Lord
  - Lamentations 3:22-23 — mercies new every morning (this is the theological basis for streak-forgiveness, §5)
- Each of the 6 categories gets one anchor verse (Spirit → John 15; Body → 1 Cor 6:19-20; Mind → Romans 12:2; Money → Proverbs 3:9-10 or Malachi 3:10; Relationships → 1 Corinthians 13; Craft → Colossians 3:23).
- Daily completion of all exercises unlocks a one-line devotional reflection tying that day's specific actions back to abiding — not generic, tied to what was actually done that day.

---

## 4. Daily exercise system

### 4.1 Structure per exercise
Each daily exercise is stored as an implementation-intention object:

```json
{
  "id": "spirit_01",
  "category": "Spirit",
  "cue": "After I silence my alarm",
  "action": "Read one verse from today's reading plan and pray one sentence",
  "duration_seconds": 90,
  "xp": 10,
  "verse_ref": "John 15:5"
}
```

### 4.2 Starter exercise set (6 categories × 1 tiny daily action each — Phase 1, weeks 1–4)

- **Spirit** — After silencing alarm → read 1 verse + 1 sentence prayer
- **Body** — After brushing teeth (morning) → 10 pushups or 20 squats
- **Mind** — After sitting down at work desk → write today's #1 priority on paper/note, one sentence
- **Money** — After opening banking app once daily → log any spend from the last 24h in one line
- **Relationships** — Before bed → send one message of appreciation/check-in to wife or a friend
- **Craft** — After lunch → 10 minutes of Spanish practice or a T24/Snowflake learning note

Phase 2 (weeks 5–8) increases duration slightly (e.g. pushups → 15, Spanish → 15 min) only after a category hits a 10-day completion rate above 80%. This mirrors progressive overload and avoids Fogg's core failure mode: don't scale up before the behavior is automatic.

### 4.3 Editability
User must be able to edit cue/action/duration per exercise from a settings screen — this is a personal tool, not a fixed curriculum. Do not hardcode the above as immutable; store as default seed data in `localStorage` on first load.

---

## 5. Gamification & scoring

### 5.1 XP and Levels
- Each completed exercise = its XP value (default 10).
- Level thresholds: simple escalating curve (e.g. Level 1 = 0 XP, Level 2 = 300 XP, Level 3 = 700 XP...). Keep numbers small enough that a level-up happens roughly weekly at full completion, to sustain motivation without inflation.

### 5.2 Streaks — with mercy built in (Lamentations 3:22-23)
- Track a per-category streak and an overall "full day" streak (all 6 done).
- **Grace day mechanic**: each user gets 2 "grace days" per rolling 30-day window where a missed day does NOT break the streak — logged distinctly (e.g. a small dove/olive icon instead of a red break), explicitly framed in copy as "mercies are new every morning — this is not a failure, it's grace used well."
- Beyond grace days, a missed day reduces the streak count but never zeroes total XP or level — total progress is never erased, only the current streak resets. This reflects the design principle in §2.4 and avoids reinforcing an all-or-nothing mindset that has historically derailed Matty's projects.

### 5.3 Weekly Sabbath review (not a 7th daily grind day)
- One day per week (user-selectable, Sunday default) the app switches to a **Review Mode** instead of daily-exercise mode: no new tasks, just a short reflection screen — "What did abiding look like this week?" with 3 short prompts (Spirit/Body/Mind, Money/Relationships/Craft) and a read-only weekly stats summary (completion %, streaks, XP gained). No pushups, no logging — a genuine rest day, theologically deliberate (Sabbath), not a scheduling gap.

### 5.4 Badges (light touch, not central)
- Small set tied to formation milestones, not vanity metrics: "7-Day Abider," "One Month in the Vine," "Full Six" (all categories same day), "Grace Received" (used a grace day and continued next day). Avoid over-designing this — it's a support mechanic, not the point.

---

## 6. Screens (minimum set)

1. **Home / Today** — today's 6 exercises as tappable cards (cue + action + checkbox), current streak, current level/XP bar, today's verse.
2. **Progress** — simple charts (per-category completion over last 30 days; can use plain SVG bars, no chart library needed for a single-file app) + level history.
3. **Settings** — edit exercises (cue/action/duration/XP), edit reading plan / verse rotation, edit grace-day count, export/import data as JSON (for backup, since it's localStorage-only).
4. **Review Mode** — the weekly Sabbath screen (§5.3).
5. **Onboarding (first run only)** — one screen explaining the six categories, John 15 framing, and that this app exists to build the discipline muscle before any bigger app gets built.

---

## 7. Technical requirements

- Single HTML file, inline `<style>` and `<script>`, no external dependencies except optionally a webfont loaded via base64 (matches his established pattern — do not use Google Fonts CDN links, embed if a custom font is wanted; system font stack is also acceptable and simpler).
- **Light theme by default.** Clean, calm, high-contrast, generous whitespace — this should not look like a generic dashboard or habit-tracker template. Add a manual dark-mode toggle (persisted in the same localStorage state blob) for evening use, off by default. No gradients-as-decoration, no glassmorphism, no generic AI-app look. Use the UI/UX Pro Max skill (installed at project start) to pick an intentional style/palette/type system rather than defaulting to generic Tailwind blues or template card-shadows.
- All state in `localStorage` under a single namespaced key (e.g. `abide_app_state`), stored as one JSON blob, not scattered keys.
- Must handle day-rollover correctly (checking "today" against local device date, not UTC, to avoid streak bugs at midnight).
- No login, no backend, no network calls. Fully offline-capable.
- Export/import JSON for manual backup between devices (he works across Mac personal / Windows work — this app is personal-side, Mac).

---

## 8. What this app is explicitly NOT

- Not a Bible study app (that's a separate existing project — Proverbs study app).
- Not the budget app (separate project, Christian stewardship-grounded, already in progress).
- Not a fitness tracker replacing his existing training log/DEXA-informed meal plan work.
- Not a habit app with 20+ configurable habits — deliberately capped at 6 (one per life domain) to keep daily cognitive load near zero, per Fogg's ability-over-motivation principle.

The explicit goal: run this for the rest of 2026 (through December), building the actual muscle of daily follow-through, before starting the next bigger build.

---

## 9. Success criteria for the build

- Opens instantly in browser, no setup.
- Today screen completable in under 2 minutes total across all 6 exercises.
- Streak/grace logic survives a closed-tab / next-day reopen correctly.
- Data survives browser refresh (localStorage persistence verified).
- Visually calm — this should feel like a quiet daily discipline, not a dopamine-slot-machine app.
