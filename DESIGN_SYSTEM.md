# DESIGN_SYSTEM.md — nabd

Personality: defined by the project's **Claude Design** system (the source of truth for the
palette, fonts, and scales). Components never hardcode visual values — everything below is a
token. New need → new token, never a magic value.

> **Source of truth & import.** The concrete token values (hex colors, font families, exact
> scales) live in the Claude Design project:
> `https://claude.ai/design/p/e42ff72c-8bbf-45a9-9481-a8f8acbbd452`. They are imported into
> this repo via the `claude_design` MCP (`/design-login`, which needs an interactive
> terminal) — see ticket **NBD-3**. This file is the contract every component codes against;
> ticket NBD-3 fills the value tables below from the design project and this doc is then the
> local source of truth. **No UI ticket starts before NBD-3 lands the real tokens.** Do not
> invent substitute colors or fonts in the meantime.

## Colors

Components consume **semantic tokens only** — never a raw ramp step or a hex literal. The
token set below is fixed; NBD-3 fills the light/dark hex values from the Claude Design project
and records the contrast ratio next to each foreground/background pair.

Required semantic tokens (light **and** dark): `background`, `surface`, `surface-raised`,
`primary`, `primary-foreground`, `accent`, `accent-foreground`, `muted`, `muted-foreground`,
`border`, `ring`, `success`, `warning`, `destructive`, `destructive-foreground`.

Exposed as CSS variables in `app/globals.css` under `@theme inline`, wired to Tailwind
utilities. Contrast bar: body text ≥ 4.5:1, large text / UI ≥ 3:1 — each pair's measured
ratio is stated here once NBD-3 imports the values; any pair that fails is corrected in the
design project, not shipped.

## Typography

nabd uses **multiple faces, one per context** (per the design decision — the design project
defines them). One usage context = one font.

| Utility | CSS var | Usage context |
| --- | --- | --- |
| `font-quran` | `--font-quran` | Quran and adhkar text (the recitation content) |
| `font-heading` | `--font-heading` | headings and section titles |
| `font-sans` | `--font-sans` | UI / body text |

Fonts load via `next/font` in the root layout and inject the CSS variables above. The exact
families come from the Claude Design project (NBD-3). Type scale: filled from the design
project as rem values (`xs … 4xl`); until then, code against the utility names, not raw sizes.

## Spacing, radii, elevation

- **Spacing** — Tailwind's 4px grid; the allowed step set is confirmed against the design
  project in NBD-3.
- **Radii** — one radius personality from the design project (sharp / soft / pill), exposed as
  `--radius`. Confirmed in NBD-3.
- **Elevation** — at most three shadow levels, tinted toward the primary hue. Values from the
  design project (NBD-3).

## Dark mode

Light + dark from day one. Mechanism: CSS variables switched by a `.dark` class on the root
(shadcn/ui convention). Dark mode is **not** inverted light — the design project defines a
dedicated dark palette (reduced saturation, tinted-not-pure-black background). Components
reference semantic tokens only, so they get correct colors in both modes for free.

## RTL rules

Default direction is **RTL** (Arabic-only). RTL-first is a hard rule:

- Use CSS **logical properties** everywhere: `ps- pe- ms- me- start- end- text-start
  text-end rounded-s- rounded-e-`.
- **Banned:** physical directional classes — `pl- pr- left- right- text-left text-right
  rounded-l- rounded-r-`. Lint should flag these.
- Directional icons (chevrons, arrows) get `rtl:rotate-180`.

## UX states

- Every data-bound view has a **skeleton** loading state (Dexie `useLiveQuery` returns
  `undefined` while in-flight — render the skeleton, never coerce to null).
- Every route segment that can fail has an **error surface** (`error.tsx`).
- Async buttons show an **in-flight** state and **block double submits** (an `inFlight` ref
  guard, per `docs/stack.md` §3).

## Accessibility

Accessibility is a **hard requirement**, not best-effort (WCAG AA):

- Semantic HTML (real `button`, `nav`, `main`, headings in order) — not `div` soup.
- Fully keyboard reachable; visible focus ring on every interactive element (the `ring`
  token).
- Color contrast meets AA (see Colors).
- Icon-only controls (e.g. the dhikr counter tap button) have accessible names.

## Signature

The dhikr **counter** is nabd's signature surface: an oversized, calm tap target with a large
live numeral, where completing the count visibly flows into the wird checklist (the counter
and the checklist are one connected motion). The exact treatment (numeral scale, the
completion transition into the checklist) is realized from the Claude Design project in NBD-3
and recorded here as the app's one distinctive move.
