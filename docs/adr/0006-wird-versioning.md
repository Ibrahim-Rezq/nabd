# ADR-0006 — Versioned wird model (malleable wird)

- **Status:** proposed
- **Date:** 2026-07-13

## Context

A user's wird is not fixed. Over time they add or drop parts (5 prayers without sunan → later
with sunan; a Quran portion of 1 juz → 2 juz). The product requires that **statistics stay
correct across these changes**: growing your wird must not retroactively make last month look
incomplete, and shrinking it must not erase past effort. This is the single hardest data
decision in nabd, and `stats/logic.ts` cannot be written correctly until it is settled.

This ADR is **proposed, not accepted** — it records the constraint and the shape of the
solution. The concrete model is decided (and this ADR moved to `accepted`) before any
statistics or checklist-persistence code is written, per the workflow's "open design question
→ ADR first" rule.

## Decision (to be finalized)

Direction: store the wird definition as **versioned records** with effective-date ranges; each
day's completion entries reference the **wird version in force on that day**. Statistics are
computed by pure functions in `stats/logic.ts` against the correct version per day, so a change
only affects days from its effective date forward. Sync (Dexie ↔ Supabase) carries versions as
immutable rows plus append-only entries, which keeps merges conflict-light.

Open questions to resolve before acceptance:

- Granularity of a "version" (whole wird vs. per-area vs. per-item).
- How a mid-day change is attributed (start-of-day snapshot vs. timestamped).
- Entry ↔ version reference shape and how it survives offline creation + later sync.

## Consequences

- `stats/logic.ts` is pure and takes `(entries, versions, day)` — testable with property-based
  tests asserting "a past day's stats never change when a new version is added."
- The Dexie schema and Supabase tables must model versions as first-class, immutable records.
- Until this ADR is accepted, statistics and durable checklist persistence are blocked.
