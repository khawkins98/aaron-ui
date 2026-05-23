<!--
NAME CANDIDATES (undecided — pick before publishing). Researched 2026-05 (availability + collisions).

AVAILABILITY AT A GLANCE
  npm: ALL six candidates are unpublished/free. GitHub handle/org: ALL five are free (404).
  Domains (.com): scriptoscope.com TAKEN (2024) · kaleidoscript.com TAKEN (2023) ·
                  schemeoscope.com / themeoscope.com / vibeoscope.com FREE.
                  (.dev/.app: registry whois was inconclusive here — verify at a registrar.)

KEY INSIGHT FROM THE RESEARCH
  - "Kaleidoscope" is an ACTIVE commercial macOS diff/merge tool (kaleidoscope.app, subscription, v5),
    well-known in the *exact* Mac-dev audience this post targets. Any "Kaleido-" name risks reading as
    affiliated with it — a real confusion/trademark concern beyond the original theming software.
  - The "-oscope" suffix lives among scientific instruments (oscilloscope / vectorscope / videoscope /
    thermoscope / Chemiscope / CymaScope), NOT theming tools — so it reads as charming homage to that
    family, not a collision. Reinforces the "an instrument you look through to see the old themes" idea.

RANKED (research-informed; was Scriptoscope-first, now Schemeoscope-first on availability + accuracy):

1. Schemeoscope — CLEANEST SLATE: name/.com/npm/GitHub all free; no real-world namesake found
     (search only turned up generic "Scheme It", oscilloscope VSTs, Chemiscope/CymaScope as cousins).
     + most ACCURATE to the project: Kaleidoscope themes are literally called "schemes"
     + instrument-suffix homage without touching the Kaleidoscope name → safest on the trademark front
     - loses the explicit JavaScript pun; mild "Scheme (the language)" overload (no actual collision found)
2. Scriptoscope — best JS pun + instrument homage; canonical one word, wordmark = script_o_scope / script-o-scope
     - scriptoscope.com is TAKEN (2024) → would need .dev/.app or another TLD
     - minor existing namesake: a content-design group (Leo Falcão); "Scripto" root is crowded
       (Scripto teleprompter app, Scripto lighters) — not our space, low but nonzero confusion
     - keep underscores for the LOGO only; plain "Scriptoscope" for domain/npm/handle/speech
3. Themeoscope — clear + .com/npm/GitHub free. - generic; drops the JS pun.
4. Vibeoscope  — clear + .com/npm/GitHub free; maxes the vibe-coding gag. - thin: loses both Kaleidoscope AND JS.
5. Kaleidoscript — DEMOTED by the research. .com TAKEN (2023); name already crowded — a literary magazine
     PLUS two JavaScript visualizers (a music visualizer + an animated image generator) live in our exact
     space; and the broader "Kaleidoscope" diff-tool trademark shadows it. Max recognition, least distinct.

SUGGESTION: lead with Schemeoscope (or Scriptoscope on a .dev/.app) and recover the lost "instant
Kaleidoscope recognition" in the subtitle ("a Kaleidoscope theme engine for the web"). Avoid "Kaleido-*".
-->

# Blog post outline — working draft (name TBD — see candidates above)

> **Status:** scaffold / outline only. Not committed to the project docs (this is
> personal writing material, not product documentation). Voice = playful,
> self-aware, technically honest. Lean into "this is gloriously stupid AND it
> actually works." Fill the beats with prose later.

---

## Working title & framing

**Lead candidate:** *Kaleidoscript* — Kaleidoscope × JavaScript.

Subtitle / tagline options (pick one, A-test them):
- "What if a theming engine from 2001 could dress up the modern web — through the magic of JavaScript and good vibes?"
- "Resurrecting a quarter-century-old Mac theming engine, one vibe-coded part-code at a time."
- "Make Gmail look like it's running Mac OS 8. Yes, on purpose."

Naming notes (for a short aside or footnote, not the body):
- The "vibe coding → good vibes" pun is the throughline — the project was largely AI-assisted ("vibe-coded"), but kept honest against the actual disassembly. That tension *is* the story. Don't overplay the pun; let it recur lightly.
- The project's current name is **Aaron UI** — a deep-cut nod to "Aaron," Apple's internal codename for the Mac OS 8 Appearance Manager. Fun lineage beat: moving from an insider in-joke (*Aaron*) to a legible pun (*Kaleidoscript*). *(Verify the Aaron/Appearance-Manager codename claim before publishing.)*
- Consider a one-line nod that the name riffs on Kaleidoscope out of affection, not appropriation (see Ethics section).

---

## 1. Cold open — the ridiculous demo

- Open with the payoff, not the backstory. A screenshot/GIF of something everyone knows — Gmail, GitHub, a news site — wearing a full Kaleidoscope scheme (BeOS, or something gloriously loud).
- One or two sentences: yes, that's a real modern website. No, it's not CSS cosplay — it's the *actual* 2001-era theme art, rendered by its *actual* layout engine, in your browser.
- Set the tone: "This is utterly stupid, slightly ridiculous, and I can't stop grinning about it."

## 2. For the kids — what *was* Kaleidoscope?

- The nostalgia hit. Kaleidoscope: a system-wide theming engine for classic Mac OS (7/8/9), shareware, with a sprawling community of "schemes" that re-skinned every window, button, scrollbar, and menu.
- The scene: people *made* these. Hundreds of them. Archived today on Mac Themes Garden / Macintosh Garden. A whole lost folk-art tradition of desktop customization.
- The gut-punch: there almost certainly hasn't been a *new* Kaleidoscope scheme rendered in anger in 15–20 years. The engine that drew them is long dead. The art survives; the thing that brought it to life doesn't.

## 3. The stupid idea

- "What if we could bring it back — not on a Mac, but on the web?"
- The vibe-coding angle: this is a hobby project, built fast and loose with AI assistance ("good vibes"), but the joke only lands if it's *real* — so it had to actually be faithful, not a hand-waved retro filter.
- Frame the ambition honestly: not "rebuild Kaleidoscope," but "build a bridge so Kaleidoscope's themes can breathe again, somewhere they were never meant to run."

## 4. What it actually does (the part that makes it not-a-toy)

- It renders real Kaleidoscope schemes **1:1 from their own binary resources** — the `cicn` artwork, the `wnd#` layout recipe, the `cinf`/`Colr` metadata. It does *not* hand-author a "Platinum-ish" CSS theme.
- The principle: get the *engine* right once, and every scheme renders for free. The renderer is a faithful replay of the thing that originally drew these windows.
- Name-drop the corpus that already works: `1138`, `1984`, `1990`, `apple-platinum-2`, `beos-r503`, `evolution`. (Pick the most visually striking for screenshots.)

## 5. The fun part — binary archaeology (the journey)

*This is the technical heart. It's a great story; tell it as one.*

- The chrome is drawn by Kaleidoscope's **kDEF** — a 68k `WDEF`, a chunk of ancient Mac assembly. To render faithfully, you have to understand what that code *did*.
- The clean-room rule (state it plainly, it matters): we **never run** the original 68k. We read the disassembly to *understand* it, then reimplement the behavior in our own TypeScript. Mimic, never execute.
- The plot twist: we decoded the **wrong version first** (Kaleidoscope 1.8.2), chased a layout model that wasn't in that binary, and burned real time on a plausible-but-wrong theory. The breakthrough was realizing the schemes we cared about use the **2.3.1** engine — which has a completely different, cleaner model: a **part-code jump table**.
- The recurring lesson, and a good pull-quote: *almost every clever heuristic we added was later deleted once we understood what the binary actually did.* Fidelity made the code **smaller**.
- The vibe-coding tie-back: AI got us moving fast, but the only thing that kept it honest was checking every claim against the actual assembly. Good vibes, verified.

## 6. The authenticity flex — there is no hover

- The detail that delights people: Mac OS 8 chrome had exactly **three** control states — Normal, Pressed, Disabled. No "hover." That's a post-OS X, web-era idea.
- So pointing at a close box looks identical to pointing anywhere else. It feels "wrong" to modern reflexes — and that wrongness is the point. It's authentic, not lazy.
- Good little riff on how much of "modern UI feel" is muscle memory we forget is a choice.

## 7. The wild use cases

- **Your own site.** Drop it in, pick a scheme, your blog now looks like a 2001 Mac. The dream end-state: just add **data attributes to your HTML** and the JS theme layer hooks in — no framework, no build step required.
- **The chaos option — userscripts.** Via GreaseMonkey / Tampermonkey, inject a scheme into sites you don't own. Gmail in BeOS. GitHub in evolution. Your doom-scroll feed wearing a 24-year-old skin. (Screenshot gallery goes here — this is the shareable bit.)
- Keep it honest: some of these are "today," some are "the architecture is aimed there, with bridges still to cross."

## 8. The honest caveats & ethics (do not skip)

- This is a **non-commercial, open-source hobby project.** Nobody's making money. Nothing here is for sale.
- **It does not replace Kaleidoscope, or the themes.** It's a bridge — a way to let these look-and-feels live in a modern context, nothing more.
- **Respect for the originals:** I reached out to the original Kaleidoscope authors and didn't hear back. If that's you — I'd genuinely love to talk. (Soft, sincere, not performative.)
- **Clean-room & provenance:** we never use Kaleidoscope's source code. We extract assets only from freeware-with-redistribution schemes, each carrying its original author, source, and license. Apple's own themes are deliberately out of scope.
- The door stays open: nothing here stops you from buying Kaleidoscope, paying the shareware license, and making a brand-new scheme. If anything, maybe this nudges someone to.

## 9. Where it's at, and the bridges left to cross

- Honest status: window chrome renders faithfully (the v3 "part-code compositor"); in-window controls are partway; the drop-in data-attribute integration is the target, not fully there yet.
- A short "what's hard / what's next" list — readers who like this *really* like this, and the honesty earns their trust (and maybe their PRs).

## 10. Outro — good vibes, come say hi

- Recap the one-liner: a quarter-century-old theming engine, resurrected on the web, faithfully enough to be ridiculous.
- Links: live demo, the repo, how to try a userscript.
- The ask: if you find this as stupid-and-cool as I do, I'd love feedback. (And: help me find the original authors.)

---

## Appendix — production notes (delete before publishing)

**Screenshots to capture:**
- Hero: a famous site (Gmail/GitHub) in a bold scheme — the "wait, what?" image.
- A side-by-side: the same window in 2–3 different schemes (sells "the engine, not a theme").
- A "no hover" micro-demo (before/after a click — nothing changes on hover).
- The corpus lineup (one window per scheme).

**Pull-quotes / lines to keep sharp:**
- "Mimic, never execute."
- "Almost every clever heuristic got deleted once we understood the binary."
- "Good vibes, verified against the assembly."
- "It's a bridge, not a replacement."

**Tone guardrails:**
- Self-aware and warm, never smug. The ridiculousness is affectionate.
- Technical bits should feel like *show-and-tell*, not a paper. Short. Concrete.
- Don't oversell the use cases that aren't built yet — label them as aspiration.

**Open questions for you (the author):**
- Commit to the *Kaleidoscript* rename, or keep *Aaron UI* and use Kaleidoscript only as the post's framing?
- How much disassembly detail does the audience want — a taste, or a real teardown (maybe a follow-up "deep dive" post)?
- Where does it publish (personal blog / dev.to / Hacker News framing)? Affects the title and the cold open.
- Are we comfortable publicly showing third-party sites (Gmail/GitHub) reskinned, given the userscript angle? (Probably fine — it's client-side and personal — but worth a sentence acknowledging it.)
