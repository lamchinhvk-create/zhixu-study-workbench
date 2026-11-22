# UI refinement · Editorial study desk

This branch is a visual and motion pass over the existing Zhixu study workbench. It keeps the product's structure, copy, data model, and behavior intact.

## Direction

The original UI already had a warm study-desk identity. This pass makes that identity more deliberate:

- paper/ink palette instead of the mint gradient and generic cool white;
- a display serif voice for page titles, auth headings, and the notebook desk;
- a single deep forest green for primary actions, with copper for citations and accents;
- calmer surfaces: fewer colored glows, consistent radii, and warmer neutral elevation;
- the constellation graph moves from navy-blue to ink-green so it feels like the same world as the rest of the app.

## What changed

- `web/index.html`: one reviewable style block, `#editorial-ui-refinement`.
- No backend, API, storage, layout, copy, or dependency changes.
- No new font or image downloads; the display face uses locally available serif fallbacks.

### Motion

- page/view entrance: 260 ms, opacity + 5 px rise;
- auth card and auth shell entrance;
- constellation reveal: one authored moment, 480 ms;
- citation drawer, modal, and toast transitions;
- hover/press feedback on primary actions and graph nodes;
- full `prefers-reduced-motion: reduce` path that removes movement while preserving state feedback.

## Verification

Run from the repository root:

```powershell
python -m venv .venv
.venv\Scripts\python.exe -m pip install -r requirements.txt
.venv\Scripts\python.exe -m uvicorn app:app --host 127.0.0.1 --port 8788
```

Checked with Microsoft Edge/Playwright at:

- 1440 × 900: login, chat, knowledge library + constellation, notebook, assignment;
- 1280 × 800: knowledge library;
- 390 × 844: login;
- no page errors, no horizontal overflow on the auth page;
- `prefers-reduced-motion: reduce`: computed `animation-name` is `none` for the auth card.

## Intentional choices

The Impeccable detector reports the existing cream palette, the constellation's dark halo, and the notebook's ruled-paper stripes. These are deliberate parts of the product world:

- the cream/paper surface is the study-desk metaphor;
- the dark constellation is a focused reading mode inside the light workspace;
- the ruled notebook is the existing `scholar-notes` pattern and is left intact.

The detector was run once; no new dependencies or behavioral changes came out of it.

## Screenshots

- `login-before-after.png`
- `library-before-after.png`
- `notes-before-after.png`

Demo data in screenshots is synthetic; no user documents or keys are included.
