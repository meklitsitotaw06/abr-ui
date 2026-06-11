# ReMapped — Prototype Handoff

A hi-fi, clickable prototype for **ReMapped**, a mobile app for people living with **phantom limb pain**.

- **Client:** ABR (prosthetics org / charity working with amputee athletes)
- **Build team:** FortyAU
- **Status:** design + interactive prototype (no backend). Used to align with the client and gather feedback.
- **This file lives with:** `phantom-limb-prototype.html` (the prototype) in the `ABS/` folder.

---

## What the product is

ReMapped is **not** trying to cure phantom limb pain. It targets the **helplessness and frustration** around it by:
1. Giving the user something to *do* in the moment of pain (fast episode logging).
2. Surfacing generally-accepted **things to try** (not diagnosis).
3. Quietly building a **journal** that improves conversations with the care team — and, aspirationally, surfaces patterns over time.

The name **ReMapped** references the neural *remapping* at the heart of phantom limb pain and its therapies (mirror therapy, desensitization). Earlier working name was *PhantomEase* — you'll still see that in some exploration files (see below).

### Users
- **Hero persona:** high-activity lower-extremity amputee (athlete).
- **Mass-market reality:** older amputees (≈80% of amputations are older diabetics), often less tech-savvy, frequently supported by a caretaker.
- **Lower-extremity only.** Upper-extremity is out of scope.
- **Core design tension:** must work for a 32-year-old triathlete *and* a 72-year-old with a caretaker. Resolved with large type, big touch targets, high contrast, and infographic-clear data.

---

## How to view it

It's a **single self-contained HTML file** — no build step, no dependencies beyond Google Fonts (loaded via CDN).

- **Quickest:** open `phantom-limb-prototype.html` in a browser.
- **Local server (used during build):** from the `ABS/` parent dir, `python3 -m http.server 9999`, then open `http://localhost:9999/ABS/phantom-limb-prototype.html`.

**Prototype map:** the dark panel pinned top-left is a **dev-only navigation aid** — it jumps to any screen. It is *not* part of the app. The real in-app navigation is the bottom tab bar (Home · Insights · Resources · Profile) plus the flows.

---

## Screens & flows

| Screen | Notes |
|---|---|
| **Splash** | Branded teal→navy launch screen; auto-advances to onboarding. |
| **Onboarding** | 2 steps. **About you** (who's using: self/caretaker · amputee's age · phantom-pain meds). **About the amputation** (per-limb: side / level / date — add multiple limbs for bilateral). |
| **Home** | Dark "Log pain" hero (primary action), quiet "days since last episode" line, daily check-in faces, recent episodes list. |
| **Log episode flow** | 7 steps: limb → severity (faces) → pain type → duration & onset → context toggles → what you tried → optional photo. Steps 3–5 are skippable. Ends on a full-screen "Episode saved" success → lands on **Insights**. |
| **Insights** | Trend chart / Calendar toggle (same height, no content jump). "What your worst days share" pattern callouts. **Share** section = one **Export & share** button → PDF → native OS share sheet (mock). |
| **Day detail** | The journal entry behind a tapped data point (context + what was tried). |
| **Resources** | Library / Things to try toggle. Library = ABR videos/articles. Things to try = tiered if-then checklist with "did it help?" ratings. |
| **Profile** | Mirrors onboarding data: About you (logging-as + age), My limbs, Medications, Settings. |

---

## Design system ("Calm Sport")

**Palette** (CSS variables in `:root`)
- Primary teal-green: `--teal-700 #0f766e` (plus 50/100/500/600/900 ramp)
- Secondary depth: `--navy #0a2a4a` — blended into the bottom of branded gradients (splash, onboarding, hero, CTAs)
- Bright accent / "energy": `--mint #5eead4` (a.k.a. `--teal-300`) — used on dark surfaces (log-pain hero icon, saved check, splash tagline, the "Mapped" in the wordmark)
- Severity scale: green `--s1` → red `--s5`
- Surfaces light: `--bg #f4f8f7`, `--card #fff`, ink `--ink`, muted `--muted`, lines `--line`

**Brand gradient:** `linear-gradient(135deg, teal-600 → teal-900 55% → navy)` on primary buttons; a 150° teal→navy variant on the hero/log-pain card and splash.

**Typography:** **Sora** for display (wordmark, screen titles, big numbers, step questions) + **DM Sans** for body/UI.

**Logo:** "pulse" mark (dashed phantom lead-in → spike → calm resolve) on a teal squircle; wordmark **Re**+**Mapped** with "Mapped" in teal. Quiet "Powered by ABR" only (no splash takeover, no loud branding — per client).

**Key components** (all in the single `<style>` block): `.card`, `.btn`/`.btn-primary` (gradient)/`.btn-ghost`, `.chip` (+ `.chipgrid`, `.chipgrid3`, `.chips.rate`), `.selcard` (emoji + byline picker), `.face` (severity), `.toggle`, `.badge` (pills), `.medpill`, `.limbcard`, `.seg` (segmented toggle), `.steps` (progress), bottom `.tabbar`, the app header `.appheader`.

---

## Decisions worth knowing

- **Severity = color-coded faces** (Mild / Medium / Bad / Severe), not a 1–10 scale — the client disliked subjective numeric scales.
- **Per-limb model:** each amputation is its own entry (side + level + date). Bilateral = two limb cards. Mirrored between onboarding and Profile.
- **Information architecture:** Things-to-try is folded **into Resources** (segmented); Share is folded **into Insights**; there is no standalone screen or extra nav item for either.
- **Sharing = export a PDF to the native share sheet** (Messages/Mail/AirDrop/etc.). No in-app care-team contact list, no provider accounts — keeps data **user-owned** and on the HIPAA-safe side (self-reported + environmental data only, exported by the user).
- **Single theme.** An "Athlete-forward" dark variant was explored and **removed**; the app is light "Calm Sport" only.
- **Local-first** concept (cloud sync is a future "nice-to-have," not built).

---

## Open questions (for the client / next decisions)
- **Monetization:** undecided — lean free/charity vs. small fee for "skin in the game" vs. freemium.
- **Branding level:** how prominent ABR should be (currently a quiet footer).
- **Capture location-on-limb** for pain? (client to confirm if clinically worth it).
- **Tagline:** parked. Leading candidate was "Something to do when it hurts."

---

## Related files (currently in the parent `Claude/` directory, not `ABS/`)
- `docs/superpowers/specs/2026-06-09-phantom-limb-pain-app-design.md` — the design spec (deeper rationale; still titled with some PhantomEase-era notes).
- `phantomease-logos.html` — logo direction exploration (4 marks).
- `phantomease-fonts.html` / `phantomease-font-pairs.html` — typography exploration (the Sora/DM Sans pairing was chosen).

> Note: the exploration files still use the old **PhantomEase** name. Only the prototype was renamed to **ReMapped**.

---

## Tech notes
- Vanilla HTML/CSS/JS, no framework, no build. All logic is in one `<script>` at the bottom (screen routing via `go(id)`; flow state for the log steps, onboarding steps, segmented toggles, med/limb repeaters).
- Phone frame is a fixed 390×844 mock; screens are absolutely-positioned and toggled by `.active`.
- Everything is illustrative/mock data — there is no persistence or backend.
