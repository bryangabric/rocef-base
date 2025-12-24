# ROCEF Base

ROCEF Base is the **foundational frontend UI repository** for ROCEF.

It serves **two explicit purposes**:

1. The long-term base of the production ROCEF frontend
2. A stable reference implementation that defines how new pages, shells, and styles must fit into the system

This repository intentionally starts **lightweight** and **data-free**.
UI structure, shell boundaries, and styling rules are locked **before** backend integration.

---

## Core Principles

- Frontend is **static** and deployable independently of the backend
- Backend (AWS) is the **single source of truth** for rules, gates, permissions, and state
- Frontend mirrors backend logic **only for UX**
- Per-org shell access is assumed from day one
- Pilot usability is prioritized over admin density
- Executive views may prioritize visual impact over interaction density

---

## Shell Architecture (Locked Decision)

ROCEF uses **three distinct UI shells**:

- Pilot
- Admin
- Executive

**Key decision: each shell has its own layout template. There is no canonical shell layout.**

Shell templates are stored as **standalone HTML documents** so they can be opened directly via `file://`
and swapped via `<iframe>` without requiring a local web server.

---

## CSS Architecture

Stable filenames. No version numbers in filenames.

```
css/
├── core.css
├── shell-pilot.css
├── shell-admin.css
└── shell-exec.css
```

Rules:
- `core.css` defines shared primitives/components only
- Shell styles control layout/density/visual identity
- Shell styles must not assume other shells exist

---

## Versioning Rule (Locked Decision)

Stable filenames in HTML. Versioning lives in:
- file header comments
- git tags/releases
- UI footer build label

---

## Admin Shell Compatibility (Locked Decision)

The Admin shell preserves **legacy ROCEF Admin DOM + CSS** assumptions by embedding the legacy DOM
(from the legacy `index.html`) into `shells/admin.html` and importing the legacy stylesheet into
`css/shell-admin.css`. Refactoring legacy CSS is explicitly deferred.


---

## Admin Shell JS/Modal Stripping

For ROCEF Base shell validation, legacy Admin JavaScript is disabled and the legacy Preview modal markup is removed to prevent unwanted pop-ups in the standalone shell.
---

## Pilot Shell Navigation & Modes (Locked Decision)

Pilot shell is **mode-aware** and supports three primary UI modes:

1. **Dashboard**
2. **Mission Selector**
3. **Checklist Run**

Key rules:

- Pilot shell has **no left sidebar**.
- Mission Selector uses **Cancel** (not “Back”) to return to Dashboard.
- Checklist Run does **not** use “Exit”. It uses run-state language:
  - **Pause** (save state and return later)
  - **Abort** (end attempt; later will require a reason)
  - **Recover** (re-open an incomplete/paused run quickly)

A “continue last mission” concept is **not used**. Each flight has its own checklist run.
Any future “resume” behavior refers only to **resuming an in-progress checklist run**, not a past mission.
---

## Shell-Scoped Visual Identity (Locked Decision)

Visual identity is owned at the **shell level**, not globally.

- `core.css` may define structural primitives and CSS variables, but **must not impose visual themes**.
- Each shell (`Pilot`, `Admin`, `Exec`) owns its own background, gradients, and color identity.
- Pilot shell defines its background via a shell-scoped CSS variable:
  - `--pilot-bg-gradient`
  - Applied only to `body[data-shell="pilot"]`
- Admin and Executive shells remain visually isolated and unaffected.

This prevents cross-shell styling bleed and allows each user group to evolve independently.
---

## Executive Shell Visual Identity (Locked Decision)

Executive shell has a distinct, restrained visual identity focused on confidence and situational awareness.

- Executive background is shell-scoped via `--exec-bg-gradient` in `css/shell-exec.css`
- Executive pages emphasize whitespace, stable typography, and low visual noise
- Executive shell is intended to be **read-only** with ambient auto-refresh (no configuration UX)

This styling is isolated to `body[data-shell="exec"]` and must not affect Pilot or Admin.


### Executive “Hero Band” (Star Scape)

Executive shell includes a dedicated top “overview band” with a subtle star-scape style background behind KPI tiles. Implemented in `css/shell-exec.css` with CSS-only layers (no external images).



### Executive Hero Band Motion

Executive hero band includes subtle CSS-only nebula drift animation (slow) and a dense tiled starfield. This remains isolated to `body[data-shell="exec"]`.


### Executive Hero Band Tuning (v1.1.4)

Increased KPI tile contrast, dramatically increased star density (including smaller stars), and made nebula + star motion intentionally obvious for visual “WOW”.


### Executive Hero Band (Organic Stars + Milky Way)

Executive hero band uses an embedded SVG starfield for organic distribution (avoids tiling artifacts) plus a subtle diagonal “Milky Way” band. Nebula intensity is intentionally restrained.


### Exec Stars Fix (v1.1.7)

Restored the Executive hero starfield (SVG background) after a CSS refactor accidentally removed it. Stars remain crisp (no blur).


### Exec Milky Way Depth (v1.1.8)

Added subtle color noise (very low alpha blues/yellows) within the Milky Way band and introduced a faint parallel band for depth. KPI tiles made slightly more transparent and centered.


### Exec KPI Spacing + Milky Way Boost (v1.1.9)

KPI strip spacing increased and centered (space-between within max width). Milky Way band contrast increased and a thin brighter core streak was added; no blur was introduced.


### Exec Milky Way Structure Pass (v1.2.0)

Milky Way is now a structured feature: reduced background star density outside the band, added a dense band-only star texture, introduced a dust-lane (negative space), and kept nebula restrained. Removed blend-mode so the band reads clearly.


### Exec Milky Way Definition (v1.2.1)

Clarified Milky Way goal to match a photographic band: cloudy bright core + dust lanes + warm horizon tint. Implemented as a dedicated overlay layer (.exec-milkyway) so stars remain crisp while only the cloud glow is softly blurred.


### Exec Milky Way Visibility Fix (v1.2.2)

Fixed Milky Way overlay not showing due to stacking order and oversized data-URI. Added explicit z-index layering for ::before/::after/.exec-milkyway and reduced SVG size so file:// browsers render reliably.


### Exec Build Visibility Marker (v1.2.3)

Added a tiny v1.2.3 watermark in the Exec hero to confirm the correct build is loaded when testing via file://. Also added a fallback Milky Way cloud glow so the effect is visible even if the SVG data-URI layer is blocked.


### Exec Milky Way Rendering Fix (v1.2.4)

Milky Way overlay now uses pure CSS gradients (no data-URI) to avoid file:// rendering inconsistencies. Added visible build watermark on Exec hero to confirm correct build is loaded.


### Exec KPI Centering + Contrast (v1.2.5)

Exec KPI row is explicitly centered (max-width container + centered flex with gap) to prevent left drift. KPI cards use a slightly darker translucent background to stay readable over the brighter Milky Way header.
