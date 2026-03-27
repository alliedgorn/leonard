# Handoff: Day 12 Session 2 — Governance, Forge, and Pack Culture

**Date**: 2026-03-27 20:15 GMT+7
**Context**: Gorn active all session. Heavy feature requests, governance, bug fixes, and a major new feature (Forge).

## What We Did

### Governance & Rules
- Deployed Rules feature (T#360) — Decrees + Norms with pack consultation
- Deployed 9 decrees + 12 norms to /rules
- Added decree approval flow (T#370) — only Gorn can approve decrees
- Rule IDs with subtle styling (T#371)
- Updated /recap skill to auto-fetch rules from API on wakeup
- Added filtering to exclude archived/unapproved rules from recap
- Created "only relevant Beasts respond" norm after pile-on incident

### Features Shipped
- T#361 PM Board task-project linking
- T#362 Image attach in all text editors
- T#364 Prowl task ID visibility
- T#365 DM page view modes (My Chats / Beast Chats)
- T#369 Spec status enforcement (rejected->pending only via resubmit)
- T#372 Forge (fitness routine tracker) — Phase 1 with meals, workouts, weight, notes, photos
- T#373 Floating DM chat overlay on remote control

### Bug Fixes
- Nav "More" link overflow (desktop + mobile) — Dex, 3 iterations
- Beast card terminal icon navigation — Karo
- Forum typing lag with 30+ messages — Karo, 3 iterations (memoize + uncontrolled textarea + pause polling)
- Feed page empty since March 16 — switched to DB-backed aggregation

### Projects Created
- Routine Tracker / Forge (project #10)
- Den Book Native App / Capacitor (project #11) — architecture discussed, Apple Health integration planned

### Security
- Forge auth bypass (as=gorn) found by Talon/Bertus, fixed by Karo
- Forge now uses session auth + localhost-only for Sable access

## Pending
- [ ] Capacitor native app — project created, architecture reviewed, no spec yet. Gorn needs Apple Developer account decision
- [ ] Forum notification targeting — still the root cause of pile-ons
- [ ] Spec #1 (T#259 ingester) — still pending Gorn approval
- [ ] Patch management policy — post to library once finalized
- [ ] Talon on thread #285 — acknowledge his role in patch management
- [ ] CLAUDE.md standing order for rules enforcement — not yet implemented (recap fetches rules but doesn't force compliance)
- [ ] Duplicate rules cleanup — norm #39 and #40 are duplicates (one Beast responds)

## Decrees This Session
- Decree approval flow — only Gorn can approve decrees

## Norms This Session
- Only relevant Beasts respond — no pile-ons
- Broader: not every message needs a reply from every Beast

## Next Session
- [ ] Run /recap to orient
- [ ] Check scheduler for due items
- [ ] Check forum/DMs for activity
- [ ] Follow up on Capacitor project — does Gorn want to proceed?
- [ ] Clean up duplicate rules (39 vs 40)
- [ ] Consider CLAUDE.md rules enforcement (stronger than recap)
- [ ] Apply rest-sooner: if board clear and Gorn silent, rest within 1h
