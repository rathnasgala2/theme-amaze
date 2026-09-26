# Changelog

All notable changes to `@rathnasgala2/theme-amaze` are documented here.

## Unreleased

2026-09-25 code-discipline review remediation (THD-H5): this file
previously carried three dated sub-headings under `## Unreleased` above a
`## 2.0.0 - 2026-09-22` heading, even though `2.0.0` has been on the
registry since 2026-09-22 — a state that made no sense read either way
(see the review's own explanation). The three dated entries below are
folded into this one `Unreleased` section (Keep a Changelog: exactly one
`Unreleased` section, dated headings below it), and `2.0.0`'s heading now
carries its actual release date. Everything in this section ships as the
next version; bumping `package.json`'s `version` for that release is an
owner decision (recommended: `2.1.0`, since nothing below is a breaking
change to the token/CSS-hook contract).

### Changed (second-pass review remediation, 2026-09-25)

- `.github/workflows/{ci.yml,nightly.yml,release.yaml}` re-pin the
  template sibling checkout to `d2b2f0ffc38407851e293e5a8a92d8863a0182d1
  # 2.1.0 (unreleased)`and the`theme-tooling` sibling checkout to
  `8fd9b36f85f4ae0a34dfb6ebb7c55319672071d2 # 0.1.0 (unpublished)`,
  picking up contract-driven pseudo-class admission, the icon property
  set, externalised contrast pairs (with three new adjacency floors), and
  the Playwright+axe `visual:check` harness. `stylingContractDigest`
  already byte-equalled the new pin's `catalogDigest`; no change needed
  there. Added a `visual` job to `ci.yml` (installs Chromium, runs
  `visual:check`, uploads screenshots as a build artifact).
- `color-accent`/`color-link` (both palettes) move to a lighter plum
  (`#b42e97` light, `#d350c7` dark) so the accent clears the new
  accent-on-text ≥3:1 adjacency floor; `color-surface-raised` (both
  palettes) moves to widen the surface/surface-raised adjacency to
  ≥1.3:1. All previously-passing pairs still clear WCAG 2.2 AA.
- `theme.json.slotHooks` no longer declares `landmark-main-content`: the
  CSS never targeted `#main-content` directly (THM-M3 set-equality).
- `a:visited` now renders `--gala-color-link-visited`, and `a:hover`
  thickens the underline — the closed CSS-hook grammar admits both
  pseudo-classes as of contract 2.1.0 (THD-M1).
- The `hr` divider mark is now explicitly sized and centered
  (`background-position`/`background-repeat`/`background-size`) instead
  of tiling at the element's default background size (THD-H8).
- Removed the redundant `text-decoration-line: underline` from print's
  `a` override — the non-print rule already sets it, and the print layer
  wins on any property it _does_ declare regardless (THD-L2).
- `.github/workflows/release.yaml`'s path filter now also watches
  `icons/mark.svg`, a packed file that previously could not trigger a
  release on its own (THD-L5). No dead root `package-lock.json` exists to
  remove; this repository is a closed 4-key `package.json` with no
  `scripts`/`dependencies`, so nothing under `tooling/` is packed either.
- Confirmed no theme-owned `prefers-reduced-motion` rule remains
  (THD-L1) — removed in an earlier pass; nothing left to change.

### Changed (contract 2.1.0 adoption, 2026-09-25)

- `theme.json.contractVersion` moves to `2.1.0` and `stylingContractDigest`
  now byte-equals the published contract's `catalogDigest`; `templateRange`
  (`^2.0.0`) is unchanged and still admits the template's current published
  version. `cssLayers` already excluded `gala-base` (the template's own
  layer, never a theme's to declare).
- Removed the fifth inert `outline-color` declaration
  (`#main-content` under `forced-colors: active`), the theme's own
  `prefers-reduced-motion: reduce` rule, and the duplicate `img`
  `max-width: 100%` declaration: the template's new `gala-base` layer
  (TPL-H3) now supplies all three — plus box-sizing, the skip-link
  pattern, and the real `:focus-visible` ring that finally makes
  `--gala-color-focus`/`--gala-focus-width` paint (THD-H1/THA-M4 fully
  resolved: no theme-side `outline-*` declaration remains anywhere).
- Merged the heading "character" block into the base component rules
  (THA-M3): each heading is now one rule instead of two ~200 lines apart
  depending on source order, and every `font-size` is paired with an
  explicit `line-height`.

### Changed (THA-H1, 2026-09-25)

- Converted the heading scale, body paragraphs, list items and code/pre
  blocks to `clamp()`-based fluid sizing instead of a fixed-rem ramp
  scoped to headings only, so the scale moves smoothly between a phone
  and a desktop viewport. Body text/list items step from 1rem to
  1.0625rem with a slightly looser 1.7 line-height, bringing the 44rem
  measure's desktop line length closer to a comfortable 65-70 characters.

### Changed (THA-M1, THA-M2, 2026-09-25)

- `heading-6` no longer sets `text-transform`/`letter-spacing`; the
  uppercase/tracked eyebrow treatment moves to the `article-preamble`
  slot, which already carried this theme's italic lead. `heading-6` keeps
  a bold weight and a font-size floor above body's ceiling.
- `color-accent`/`color-on-accent` now render on a real surface — the
  appearance control's background/border/text and the `article-end`
  divider's border color — instead of being declared and unused.

### Changed (THD-H8, THD-M1, THA-L1, 2026-09-25)

- Added `icons/mark.svg`, a sanitiser-clean passive SVG asset (this
  theme's one reference icon), referenced from the `hr` hook as a small
  repeating ornament. `color-surface-raised`/`space-3`/`space-8` now back
  the `blockquote` hook's background/padding and the `article-end` slot's
  top margin. `color-link-visited`/`color-success`/`color-warning` remain
  unreferenced — no admitted selector can target a visited link yet (the
  closed CSS-hook grammar does not parse pseudo-classes), and no
  `publicThemeSlotHooks` atom exists for a success/warning surface.
- `heading-1`-`heading-3` now carry graded negative letter-spacing instead
  of a single fixed value on `heading-1` only (THA-L1).
- The internal ticket id previously carried in the character-block
  comment (THA-L2) is gone as a side effect of the THA-M3 merge above;
  the comment it named no longer exists.

### Changed (pins, 2026-09-25)

- `.github/workflows/{ci.yml,nightly.yml,release.yaml}` pin the template
  sibling checkout to `e66d8771189966db1f8f876b005ab59d4f676bcb # 2.1.0
(unreleased)` and the `theme-tooling` sibling checkout to
  `68dceb301c071f3a60c2bf4c4f3215a6c3478502 # 0.1.0 (unpublished)`.

Recommended release for everything in this section plus the prior
`Unreleased` entries below: **2.1.0** (minor) — contract 2.1.0 adoption,
the fluid type scale and the reference icon are additive; nothing here
removes or renames a published token, hook or file.

### Changed (THD-H1, 2026-09-25)

- Removed the four inert `outline-color`/`outline-width` declaration pairs
  from `components.css` (`#main-content`, `a`, `select`) — `outline-style`
  was never set alongside them, so they painted nothing (the initial value
  of `outline-style` is `none`), and the previous README/CHANGELOG claim
  that they produced a themed visible focus ring was false. A themed ring
  needs `:focus-visible`, unavailable in this template contract version
  (TPL-H2); a single comment in `components.css` documents where it will
  be restored.

### Changed (THD-C1, 2026-09-25)

- Added a bare-root `[data-gala-publication-root]` block (light palette)
  plus a `@media (prefers-color-scheme: dark)` override to `tokens.css`,
  before the two resolved-mode blocks, so every `--gala-*` token still has
  a real value when `data-gala-resolved-color-mode` is not set (no
  JavaScript, a text-mode crawler, or a pre-hydration paint) — previously
  the theme applied no styling at all in that case.

### Changed (THD-M6, 2026-09-25)

- Replaced this repository's own copy of `tooling/scripts`/`tooling/test`
  (25 files, identical across all five theme repositories except one
  package-name literal, and the `tooling-drift.test.mjs` guard that
  skipped in every CI configuration these repositories had, THD-H3) with a
  dependency on the new `@rathnasgala2/theme-tooling` repository, which
  now implements every gate once. `tooling/` here carries only
  `run.mjs` and a trimmed `package.json`. See
  `../theme-tooling/CHANGELOG.md` for what moved and what changed in the
  process (THD-H2/M2/M3/M4/M5).
- Deleted the root `package-lock.json` (THD-L5): the published
  `package.json` has never had a dependency for it to lock.
- Widened the closed `package.json` shape to carry `repository` (THD-H6):
  `npm publish --provenance` derives the source repository from that
  field and refuses to build a provenance statement without it.

### Changed (SCHEMA-REPIN-2.11.0, 2026-09-22)

- `tooling/package.json` re-pins `@rathnasgala2/schemas` from the LOCAL-1
  local tarball (`file:../../../local-packages/rathnasgala2-schemas-2.8.0.tgz`)
  to the exact published registry version `2.11.0`
  (`https://registry.npmjs.org/@rathnasgala2/schemas/-/schemas-2.11.0.tgz`,
  integrity `sha512-5hXxpLaXqEKKhoRLBBEq98rzJQ9K4u3b8nDMt/ZZmV2gL4XRmTOCwjF1U618UJ1CgmFnlifhQWRuDvQQVyFfTA==`).
  This fixes CI, which was failing on every push because the `file:` path
  does not exist on GitHub Actions runners. `urn:gala:schema:theme-contract:2.0.0`
  and the `build-input` root this tooling validates against are
  byte-identical between 2.8.0 and 2.11.0 (contract re-pin packet,
  2026-09-19); `tooling/package-lock.json` and `sbom.cdx.json` regenerated
  accordingly; full `npm run verify` re-run and green.
- Added `tooling/scripts/check-no-local-schema-pin.mjs` (wired into
  `verify` as `schema-pin:check`) so a `file:`/`local-packages` specifier
  for `@rathnasgala2/schemas` can never silently return.

### Changed (THEMES-2.8.0, 2026-09-18)

- `tooling/package.json` pins `@rathnasgala2/schemas` to the packed
  `rathnasgala2-schemas-2.8.0.tgz` tarball (sha256
  `6352293855cdcff9054d43ced876740644f6b45bc813eda3990b646ec9bef563`,
  LOCAL-1), up from 2.6.1; `tooling/package-lock.json` integrity and
  `sbom.cdx.json` regenerated. `urn:gala:schema:theme-contract:2.0.0`, the
  `build-input` root and the published `examples/valid/build-input/canonical.json`
  this tooling validates against are byte-identical between 2.6.1 and 2.8.0;
  the 2.7.0-2.8.0 delta is confined to the deployment roots, the OpenAPI
  bundle and the App catalogs, none of which this repository consumes.

### Added (FOLLOW-UP SUPPLY-CHAIN-JS, 2026-09-17)

- `tooling/scripts/resolve-template-dir.mjs` and `tooling/test/tooling-drift.test.mjs`
  updated to `theme-default`'s canonical copies: `resolveTemplateDir()` now
  also honours `WORKSPACE_ROOT` (DEC-015 name), checked after the existing
  `GALA_TEMPLATE_DIR` override and before the fixed relative default
  (`<WORKSPACE_ROOT>/template`), fixing resolution from a git worktree one
  level deeper than the real checkout (LOCAL-38); `tooling-drift.test.mjs`
  resolves its `theme-default` canonical source the same way and reads
  `@rathnasgala2/theme-amaze`'s own package-identity literal from `package.json` at run time
  instead of a hardcoded name, and skips (with a printed reason) rather than
  failing when `theme-default` cannot be found. Added
  `tooling/test/resolve-template-dir.test.mjs`.

## 2.0.0 - Unreleased (task packet S2-T14)

### Added

- Visual character: Expressive typography scale: a large display heading scale (explicit rem font sizes on `heading-1`..`heading-6`, tightened tracking on `h1`, an italic lead on `slot-article-preamble`), roomier `space-*`/`content-measure`/`radius-*` tokens, a warm ivory canvas and a plum accent/link pair.
- Initial closed package file set: `package.json` (dependency-free,
  script-free, 4-key closed shape), `theme.json` (all 35 tokens for light
  and dark palettes, `stylesheets`/`cssLayers` three-file shape, the
  51-hook `slotHooks` subset this theme's CSS uses, budgets, and the
  digest chain), `tokens.css`/`components.css`/`print.css`, and a
  compact-JCS `LICENSE` license-evidence file (SPDX `Apache-2.0`).
- WCAG 2.2 AA contrast for every named token pair in both palettes,
  `outline-color`/`outline-width` on every interactive hook (no
  `outline-style` override, no `:focus` pseudo-class available in this
  template contract version — corrected 2026-09-25, THD-H1: these two
  longhands alone never painted a visible ring, and were removed),
  `forced-colors: active` system-color mappings, and a defensive
  `prefers-reduced-motion: reduce` rule.
- `tooling/` local dev/test/SBOM project (private, unpublished, its own
  lockfile) with the closed-hook CSS conformance test, the WCAG contrast
  test, the theme-contract schema test, the closed-package-file-set test,
  the forbidden-constructs absence test, the digest-cycle generator/test,
  the template-conformance byte-equality test (two builds against
  `@rathnasgala2/template`'s `main` branch, consumed by path), and a
  tooling-drift test asserting `tooling/scripts/*.mjs` is byte-identical
  to `theme-default`'s canonical copy except the one documented
  package-identity literal.
- SBOM (`sbom.cdx.json`, CycloneDX 1.6, generated for the published package
  surface — which has zero runtime dependencies).

### Notes

- `fixtureDigest`/`evidenceDigest` are this repository's own genuine local
  conformance evidence (five of the eight DEC-097 runner IDs:
  `schema`/`semantic`/`package`/`css`/`absence`), not the DEC-097-mandated
  _shared_ fixture release/result the not-yet-existing `S2-T11` reusable
  CI workflow will eventually produce and re-issue across all five theme
  packages. See README "What `fixtureDigest`/`evidenceDigest` are, and are
  not."
