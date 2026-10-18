# Handoff: PaisaFetch FAQ / Privacy Policy site

## Where this lives
- Repo: `DhamaGaurav/privacy-policies` (this repo), root of this working directory.
- Pages: `paisafetch/index.html` (Privacy Policy), `paisafetch/faq/index.html` (FAQ).
- Hosted live at:
  - https://dhamagaurav.github.io/privacy-policies/paisafetch/
  - https://dhamagaurav.github.io/privacy-policies/paisafetch/faq/
- Deploys automatically via GitHub Pages on push to `main` — no build step, just plain HTML/CSS.

## Current state (as of this handoff)
Everything is committed and working:
- `76b1d56` — FAQ page added, 14 sections grouped into Basics/Logging/Features/Data, each Android-only or iPhone-only feature explicitly labeled with a `.platform` pill badge (not presented as universal).
- `887ab10` — Privacy policy updated to cover Android alongside iOS.
- `a961148` + `404d610` — Fixed a real bug: the FAQ's sticky sidebar TOC overlapped the footer, and separately, its `@media (max-width: 880px)` mobile rule was silently losing to an earlier unconditional rule due to CSS source-order/specificity (a media query positioned before the plain rule it's meant to override loses regardless of the media condition). Fixed by adding `max-height`/`overflow-y` to the TOC and moving the media-query block to the end of the stylesheet on both pages. **Verified live** at both URLs with a cache-busted fetch + mobile-viewport screenshot — TOC correctly hides at ≤880px, no overlap.

Both pages share one design system: CSS vars `--ink/--paper/--accent`, Fraunces (headings) / Public Sans (body) / IBM Plex Mono (labels) fonts, sticky grouped-link TOC on desktop.

## Nothing is currently broken or blocking
This handoff exists because Gaurav wants to keep working on the FAQ in parallel with unrelated git branch restructuring happening in the main `PaisaFetch` app repo (a different repo, different working directory) — not because anything here needs fixing. Whatever comes next is Gaurav's call; some likely directions if he doesn't have something specific in mind yet:
- Add/edit FAQ questions as real user questions come in.
- Keep the FAQ in sync whenever a feature covered by it changes on either platform (check `PaisaFetch/PROJECT_CONTEXT.md` and `PaisaFetchAndroid/` for what's actually shipped before writing a platform-exclusivity claim — don't assume from memory).
- Visual polish/design passes on either page.

## Ground rules already established this project
- Every FAQ answer that's platform-exclusive must say so explicitly (Android-only / iPhone-only), never presented as if it works the same on both — this was an explicit requirement, not a style preference.
- When editing the shared `<style>` block, remember the CSS source-order gotcha above: a `@media` override must come AFTER the unconditional rule it overrides, regardless of where it "logically" belongs in the file.
- Verify any visual/CSS fix live (cache-busted fetch of the deployed page + a real viewport screenshot), not just by reading the source — a stale browser tab can look "still broken" even after a correct deploy.
