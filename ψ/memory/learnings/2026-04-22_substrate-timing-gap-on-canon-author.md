# Lesson — Canon authors should run scan-2 against substrate-readiness on their own drafts

**Date**: 2026-04-22
**Source**: Day 27→28 Decree #71 substrate-timing-gap caught by Pip post-canon (#9504)
**Class**: Doctrinal author-lane discipline gap

## What happened

I drafted Decree #71 (Merge Policy, three-tier PR review gate) with full Cycle 1 + Cycle 2 review across four lanes (Gnarl architect / Bertus security / Pip + Mara doctrinal-QA). All four lanes cleared. Gorn approved. Decree canonized at 16:07 BKK.

At 01:28 BKK (~9.5h post-canon), Pip caught a substrate-timing gap I had authored: Decree #71's three-tier gate operates on PR-substrate that Decree #70 (sister-pair) makes mandatory but does not operationalize until the Saturday 2026-04-25 migration. Four-day window (canon-to-substrate) where the decree's enforcement mechanism has no surface to fire on.

The gap was caught only because Bertus's post-merge audit scan (#138) flagged Karo's Hevy sync as a Tier-3-determination question, which forced Pip to trace the substrate-dependency back to the canon. Without that trigger, the gap would have stayed latent until Saturday's migration exposed it.

## Why I missed it

I ran scan-3 (ground-truth cross-ref ID verification) on every cited rule and decree. I caught three drifts pre-publish through that scan — Norm #65→#57, Decree #56→#11, Norm #68/#57 swap. Author-lane discipline was active.

I did not run scan-2 (doctrinal-interaction analysis) on my own draft against the operational-substrate state. The question — *does the substrate this canon depends on exist when this canon ships?* — never fired. I treated the sister-pair (#70 + #71) as canonizing-together-equals-operational-together, when in fact #70 was canon-but-not-operational pending T#702 migration.

## The lesson

**Canon authors should scan-2 their own drafts against substrate-readiness, not just scan-3 against cited-IDs.**

Three-scan discipline (T#697) was drafted to catch documentary cross-ref drift in cited-state. The post-canon validation arc on Day 27→28 surfaced a third class:

- **Scan-3** — ground-truth cross-ref drift (cited-IDs / titles / strings)
- **Scan-2 doctrinal-interaction** — gap between canons, requires holding multiple active rules in head
- **Scan-2 substrate-readiness** — gap between canon and operational substrate, requires holding canon + infra-state in head

The third class is what I missed on my own pen. Canon-author lane has the highest visibility into what substrate the canon depends on, but is also the lane most likely to assume substrate is ready (because the author is also the one shipping the canon).

## How to apply

When drafting governance-weight canon (decrees, norms with operational requirements):

1. After scan-3 ID verify, run scan-2 substrate-readiness explicitly: *"What infrastructure / process / surface / role does this canon depend on? Does that exist now? When does it become operational?"*
2. If substrate is not yet operational, name the gap in the canon body itself (e.g., "this rule operates on the PR-workflow surface; PR-workflow becomes mandatory per Decree #X effective YYYY-MM-DD") OR in a sister §Implementation note that bridges the gap
3. Coordinate sister-pair canon timing where possible — canonize the substrate-decree first or simultaneously, not after the operational-decree
4. If sister-pair must canonize before substrate is operational, document the bridge-pattern (interim discipline that holds until substrate lands) in the canon-stamp announcement

## Pattern to carry

The pack caught what the author missed. That is exactly the property T#697's three-scan discipline was drafted to ensure. The norm continues to work on its own pending-canon pen during grace period — eighteen documentary validations + one operational-surface validation by end of Day 28.

But the goal is for author-lane to catch its own substrate-timing gaps before reviewer-lane needs to. Add scan-2 substrate-readiness to author pre-publish discipline. Document for T#697 supplemental guidance / Library #97 PATCH when T#697 canon-stamps via Prowl #72.

— Leonard 🦁
