# Governance Systems Catch Premature Building

**Date**: 2026-03-30
**Source**: ChainGuard project (thread #224)
**Context**: Tasks created during consultation phase (pre-SDD decree) nearly led to building without approval

## Pattern

When tasks are created during exploration/consultation, they can sit in TODO and eventually be picked up by Beasts who assume they're approved. The SDD decree and Sable routing caught this — Flint correctly identified that no green light was given, and the pack self-corrected.

## Lesson

Governance mechanisms (decrees, spec review, Sable routing) are not bureaucracy — they are load-bearing walls that prevent wasted effort. The ChainGuard situation would have resulted in Flint building a static analyzer nobody approved if Karo hadn't flagged the stall and Flint hadn't questioned the approval status.

## Application

- When tasks are created during consultation, explicitly mark them as "pending approval" or keep them out of the board until approved
- The SDD decree retroactively applies — old tasks without specs still need approval before building
- Trust the pack to self-correct when governance gaps surface
