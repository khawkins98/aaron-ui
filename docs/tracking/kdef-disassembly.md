# Tracker: kDEF disassembly — definitive Kaleidoscope rendering algorithm

**Status:** parked / future-work. Captured 2026-05-19 after the empirical research arc concluded.

## Why this exists

Aaron UI's chrome rendering is currently inferred from:
- The K2 Scheme Reference (Kaleidoscope's own format doc, distributed inside the 2.3.1 installer)
- The K1 Scheme Reference (older Kaleidoscope spec from the 1.8.2 era)
- Scheme Factory v1.0PR2's resource fork (the official scheme editor's UI strings + menu items)
- Cross-corpus empirical audit of 7 schemes
- Apple's documented WDEF protocol

These got us to a reasonable approximation but **the actual rendering algorithm Kaleidoscope used isn't documented in human-readable form**. It lives only in compiled 68k machine code inside the Kaleidoscope control panel's resource fork.

Specifically:
- `Kaleidoscope 1.8.2 Installer/Kaleidoscope` resource fork contains:
  - **`kDEF id=0`** named "680x0 DefProcs" — **60,732 bytes of 68k assembly** = the canonical chrome rendering algorithm
  - `kDEF id=1` — 99,960 bytes — likely additional rendering variants
  - 8 WDEFs + 14 CDEFs (Apple-protocol-compatible variants)

The kDEF type is Kaleidoscope-specific (not Apple-standard). The bytes start with a 68k branch + a literal `kDEF` self-identifier, confirming they're compiled functions Kaleidoscope dispatches at runtime.

## What disassembly would settle

Open questions our current heuristics paper over:

1. **Per-segment tile-vs-stretch rule** — for window chrome (no cinf), is stretch the literal default (per K2 Speed Note) or is there an implicit per-segment rule? Our hybrid `span > 2 → stretch full slice, span ≤ 2 → 1-px stretch` is empirically tuned, not derived.
2. **Multiple widget instances** — K2 says rectList can have duplicates that animate together. We've never seen this in the 7-scheme corpus. Disassembly would show the actual rendering path.
3. **Crumple zones** — K2 mentions end-cap segments that "disappear when the window gets too small." Mechanism unknown.
4. **Part code 18 (gradient stretch)** — documented as "scaling each pixel by the same amount" but rendering specifics unclear vs. ordinary stretch.
5. **Apple WDEF part-code mapping** — how Kaleidoscope translates its scheme-internal part numbers to Apple's `wInGoAway`/`wInZoomIn`/etc. for `wHit` responses.
6. **Recipe convention disambiguation** — when a recipe references a named widget at multiple positions, what visual + hit-test treatment does the actual binary apply?

## What disassembly requires

Estimated 1–2 days of work:

- **Tools:** Ghidra (free, full-featured) or IDA Pro (license) with 68k support
- **Method:** load the kDEF as raw 68k binary at offset 8 (skip the branch + "kDEF" sentinel); identify entry-point dispatch via the WDEF message protocol switch (`wDraw=0`, `wHit=1`, `wCalcRgns=2`, etc.); follow the wDraw branch to the actual rendering loop
- **Output expected:** a documented algorithm describing exactly which cicn pixels are sourced for each recipe segment and how they're composited

## Why parked

The current rendering is internally consistent with the public docs (K1 + K2 references) and produces visually acceptable results across the 7-scheme corpus. Disassembly would refine the few remaining heuristic-tuned cases (the span-2 threshold, the static-graphic question) but would not change the overall architecture.

The disassembly is most valuable when:
- We're confident the HTML skeleton + raster-mapping + composer specs (the three-layer abstraction) are stable
- We have a known visual reference (a real Kaleidoscope run in UTM) to validate findings against
- Phase 3 controls + hit-testing are wired (so rendering refinements can be validated end-to-end)

Until then: ship the K2-faithful implementation we have and iterate at the spec level.

## Resources

- `Kaleidoscope 2.3.1 Installer.bin` (~1.8 MB) → `Kaleidoscope/..namedfork/rsrc` — 2.3.1 control panel resource fork (~1 MB)
- `Kaleidoscope 1.8.2 Installer.app` (~186 KB) → `Kaleidoscope/..namedfork/rsrc` — 1.8.2 control panel resource fork (~500 KB). **Smaller, simpler, K1-era — recommend starting here.**
- Mac Themes Garden (https://macthemes.garden/) — scheme previews rendered by real Kaleidoscope in UTM; use as visual ground truth for comparing disassembly findings against
- `docs/aaron-ui-architecture-spec.md` — what we've inferred so far from public sources

## Owner / next step

Unassigned. Trigger to revisit: when the HTML skeleton + raster-mapping + composer specs are settled and we want to lock down the rendering algorithm precisely.
