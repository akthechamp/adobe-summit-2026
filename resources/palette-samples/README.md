# Palette Samples — Historical Research

> **Status:** ✅ Decision made — **Palette A (Warm Premium) is LOCKED.**
> See [`DECISION.md`](./DECISION.md) for full reasoning.
> See [`../brand-system.md`](../brand-system.md) for the locked brand spec.

## What's in this folder

This folder is **historical research** — preserved as the evidence trail for the palette decision. All files are kept intentionally so the decision can be re-verified or revisited later.

| File | What it is |
|------|-----------|
| `DECISION.md` | The actual decision record. Start here. |
| `preview.html` | Live side-by-side preview of all 5 palette candidates applied to the same AI Forte mockup. Open in a browser anytime to re-verify. |
| `prompt-a-warm-premium.txt` | Gemini/AI Studio prompt for Palette A (for future reference) |
| `prompt-b-monochrome-green.txt` | Prompt for B (rejected) |
| `prompt-c-adobe-adjacent.txt` | Prompt for C (rejected) |
| `prompt-d-graphite-lime.txt` | Prompt for D (rejected) |
| (Palette E) | Only documented in `preview.html` + `DECISION.md`, no separate prompt file |

## How the decision was made

1. Started with 4 palette directions (A, B, C, D) and prompts written for AI Studio generation
2. Attempted API generation → blocked by Google cutting the free tier for image models in late 2025
3. Pivoted to a **local HTML mockup preview** rendering all palettes identically side-by-side
4. User requested a 5th option (E — Aurora Glass) for liquid-glass / isometric-3D use cases
5. Added E to the preview with glass effects, gradient text, glow shadows
6. Narrowed decision to A vs E
7. Evaluated on 5 axes: sea-of-sameness, Adobe theme alignment, audience psychology, asset durability, memorability
8. **A won** on differentiation, buyer trust, and print/scale durability
9. Kept E as a hybrid tactical flourish for digital-only 3D moments

## Re-opening the preview

```bash
open preview.html
```

## Why keep all of this

- Future-proofing: if the brand ever feels wrong and we're tempted to switch, we can revisit the actual reasoning instead of second-guessing
- Explains visual choices to future collaborators (agency team, designers)
- Documents what was considered and *why* it was rejected — not just what was picked
- Supports the hybrid E flourish — if it ever gets used, the E prompt data is ready
