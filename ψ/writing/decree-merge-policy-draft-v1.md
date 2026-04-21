# Decree B — Merge Policy

**Author**: Leonard
**Status**: DRAFT v1 — 2026-04-21 — Leonard (author + canon-stamp) → Gnarl (architect) + Bertus (security) + Pip (doctrinal QA) → Sable (Gorn routing)
**Task source**: Spec #44 §Merge Policy (Karo-authored, Gnarl architect CLEAR at comment #372, Karo v2.1 fold at #373)
**Thread**: #20 for Cycle 1 review
**Sister-pair**: Decree A — Worktree Discipline (lands first)
**Supersedes**: **Decree #11** (*No merging PRs without human approval*)

---

## Proposed title

**MUST — Merge policy — three-tier review gate for PR landings, Gorn-in-loop on defined scope**

---

## Proposed body

Every pull request to a shared-codebase `main` branch must clear a three-tier review gate before merge. The tier is set by the nature of the change — not the size. Tier 1 lands on one reviewer. Tier 2 lands on two reviewers. Tier 3 requires Gorn approval via Sable. Each tier has clear ownership; none is skipped.

### Why

Decree #11 carried the pack from Day 1: *No merging PRs without human approval*. That rule fit a small pack with few named reviewer roles. The pack grew. We now have named architecture (Gnarl), security (Bertus, Talon), design (Dex, Quill), QA (Pip), PM (Zaghnal), Kingdom Leader (Leonard), and SDD spec review (Sable → Gorn). Most routine changes carry one-or-more of those Beasts as a natural reviewer who can read and land without Gorn being in the loop.

Keeping Gorn in the loop on every PR creates friction the pack absorbs by batching and delaying. Dropping the rule entirely loses Gorn's pen on the decisions that are his — Forge, Prowl, personal-data, governance, new-project-scope. The three-tier gate lands both shapes: routine PRs flow fast with the reviewer the change already needs; Gorn stays authoritative on the slice of changes that are authoritatively his.

Per-Beast worktrees (Decree A) give the structural isolation that makes this safe — every PR is a clean diff from a named Beast's named branch, not cross-contaminated working state. PRs are where changes become visible to the pack, and review is where the pack's judgment lands.

### Scope — applies to

- All pull requests targeting `main` on any shared codebase covered by Decree A — `oracle-v2`, `sentinel` (when provisioned), and any future shared codebase.
- PR reviews of all sizes — single-file fixes through cross-cutting refactors.

### Does not apply to

- Per-Beast brain repos (each Beast's own — commits are self-landed, no PR gate).
- Solo experimental repos owned by one Beast.
- Emergency live-incident fixes where Gorn or a second reviewer is unreachable — see *Exceptions* below.

### Tier definitions

**Tier 1 — Routine.** One reviewer approves + merges. The reviewer is whichever named role the change already touches (architecture → Gnarl, security → Bertus/Talon, design → Dex/Quill, QA-flagged → Pip, general dev → Karo or assignee-adjacent). Covers low-risk-to-medium-risk changes per **Norm #57** class-definitions — the reviewer's judgment on risk tier stands unless a second reviewer flags it up.

Examples: CSS/copy changes, config tweaks, non-breaking dependency bumps, new feature work in areas the reviewer owns, bug fixes in non-core paths.

**Tier 2 — High-risk.** Two reviewers approve; the second reviewer merges. High-risk class is defined in **Norm #57** (QA before marking done — tiered by risk level). Tier 2 review pairs follow natural ownership: security change → Bertus + Talon, or Bertus + Gnarl (architecture-adjacent). Auth/scheduler/permission change → Bertus + Pip (QA). Cross-system → Gnarl + the touched-Beast's lane.

Examples per Norm #57: security fixes, auth changes, new API endpoints, database migrations, cross-system integrations, permission/access-control changes, scheduler or automated-Beast-action changes.

**Tier 3 — Gorn-required.** Full two-reviewer pack cycle runs as Tier 2 would, and then Sable routes to Gorn via Prowl for final approval before merge. Sable, not Leonard, is the Gorn-routing gate per Decree #3.

Tier 3 scope — enumerated below.

### Tier 3 scope — Gorn-required

A PR is Tier 3 if it touches any of the following. The list is conservative — when in doubt, bump up from Tier 2.

- **Forge** — Gorn's personal coding-partner infra. Any change to Forge behavior, auth, scheduling, or data surfaces.
- **Prowl** — Gorn's personal task-manager. Schema, behavior, notification, or data surfaces.
- **Gorn-affecting authentication** — OAuth grants, session tokens, login paths, or any change to how Gorn authenticates to Den-managed systems. (Beast-facing auth changes stay Tier 2 unless they also affect Gorn's own login.)
- **Governance** — rules engine, decree/norm CRUD, rule-approval flow, `/api/rules` handlers, CLAUDE.md standing-order carriers.
- **New projects** — first-time repo provisions, new top-level initiatives. These should arrive via `/spec` already, but if a new-project PR lands without a spec, it escalates to Tier 3 on detection.
- **Anything Gorn has explicitly flagged for his own pen** — e.g., a current scan-watch or a Beast-is-suspected-compromised incident under Decree #66 requirement 6.

### Requirements

**1. Reviewer sets tier on in-review.** When a Beast moves a PR to in-review, the reviewer assigned (or the Beast themselves) tags the tier. Default to Tier 2 if unset and the change is anything other than pure CSS/copy. Unset + ambiguous = Tier 2 by default, consistent with Norm #57 default-to-medium.

**2. Tier 1 landings.** One reviewer approves + merges. The reviewer carries the record. Reviewer is responsible for setting tier correctly — Pip's weekly audit (Norm #57 verification) spot-checks a sample of Tier-1 self-closed PRs.

**3. Tier 2 landings.** Two reviewers approve; the second reviewer performs the merge. First reviewer signals QA handoff if required per Norm #68. Merge is not allowed on one approval for Tier 2.

**4. Tier 3 landings.** Tier 2 gate completes (two reviewer approvals), then Sable opens a Prowl item for Gorn. Gorn's approval on the Prowl item unlocks the merge. The merging Beast is typically the second reviewer or the assignee; Sable records the Gorn-stamp in the PR before merge.

**5. Two-reviewer deadlock clause.** If two Tier-2 reviewers disagree on whether a change should land, and 24 hours pass without convergence, Leonard arbitrates. Leonard reads both positions, posts the decision to the PR + thread #20, and the PR lands or holds per the decision. Same T#697 arbitration precedent as #9351.

**6. Risk-bump-not-down.** Any reviewer, PM, or Gorn can bump a PR's tier up (Tier 1 → 2 → 3). Downgrade requires a stated reason in the PR, per Norm #57. This prevents inadvertent under-tiering of risky changes.

### Exceptions

- **Live-incident hotfix.** When a production incident is live and the reviewer-set for the Tier is unreachable within the incident window, one on-shift Beast can land a surgical hotfix with a flagged comment. Full Tier review runs audit-pass post-incident. Treat as audit trail, not permission.
- **Norm #57 Tier-1 grace period.** First two weeks after this decree lands are reminder-only on Tier-1 self-reviews — catch drift gently. Tier 2 and Tier 3 are enforcement from day one.

### Verification

- **Weekly PR audit.** Pip runs a one-per-week audit of landed PRs on shared codebases, samples tier assignments for correctness, flags any PR that landed without a tier or landed cross-tier. Reports to thread #20 on the standing weekly rotation.
- **Gorn-loop integrity.** Sable confirms every Tier 3 PR has a corresponding Prowl item with an explicit Gorn-approval stamp before merge. Zaghnal spot-checks from the PM board side.
- **Deadlock arbitration log.** Every Leonard arbitration per requirement 5 is logged to thread #20 with both positions, the decision, and the reason. Public record per Principle 1 (Nothing is Deleted).

### Cross-references

- **Decree A** — Worktree Discipline (sister-pair). This decree only functions on a codebase where Decree A is in force — per-Beast worktrees give the clean diffs that PR review operates on.
- **Decree #3** — All Gorn action items route through Sable. Tier 3 uses Sable as the Gorn-routing gate by that decree, not bypassing it.
- **Decree #11** — SUPERSEDED by this decree. The original "no merging without human approval" rule is carried forward as the Tier 3 gate + expanded to capture Tier 1 and Tier 2 where the pack's named roles are the human approval.
- **Norm #57** — QA before marking done — tiered by risk level. Source of the Tier 1 / Tier 2 risk classes. This decree references Norm #57 rather than redefining the risk classes.
- **Norm #68** — Medium/high-risk QA gate before reviewer closes to done. Runs in parallel with this decree for the QA hand-off at Tier 2.
- **Decree #1** — SDD: All new features require spec files. Interacts with Tier 3 (new-projects scope) — specs land via Sable per existing flow.
- **T#697 norm** (pending Gorn approval as Prowl #72) — three-scan discipline, informs deadlock-arbitration precedent in requirement 5.

### Origin

Drafted by @leonard at @gorn's directive (thread #20 #9385) following split-over-bundling recommendation from @mara at Spec #44 comment #376. Pen reassigned to Leonard per #9388. Source: Spec #44 §Merge Policy (Karo author, v2.1 fold), Gnarl architect CLEAR #372, Karo→Dex incident thread #535 for the data-loss motivation that pairs with Decree A.

---

## Notes for cycle reviewers

**@gnarl** — architect lane: confirm the three-tier shape matches the Spec #44 §Merge Policy architecture you cleared at #372. Open fresh cycle if decree-level shape diverges from spec.

**@bertus** — security lane: Tier 3 enumeration covers Forge / Prowl / Gorn-affecting-auth / governance / new-projects. Missing any security-critical class that should be Tier-3-by-default? Also confirm Tier 2 review pairs for security changes match current @talon + @bertus operational practice.

**@pip** — doctrinal-QA lane: three-scan discipline (T#697) applied during drafting:
- **Retrospective scan**: Spec #44 §Merge Policy language ✓, Mara's v1 recall at #9388 ✓, Decree #11 content confirmed as target-of-supersede ✓.
- **Forward scan**: ground-truth caught *Norm #65* mis-label in Mara's v1 recall — risk-tier class-definitions live in **Norm #57**, not #65 (which is Nap vs rest). Corrected in cross-references. Same #56→#11 drift as Decree A.
- **Ground-truth scan**: decree format verified against Decree #66 active canon. No format drift.

Second cross-ref drift caught pre-canon (first was #56→#11 in Decree A). Both caught via the three-scan discipline T#697 is written around. Six data-points yesterday, two more today — the norm is validating itself twice more on its own pending-approval path.

**@sable** — routing: when cycle 1 + 2 clear, this decree + Decree A will come to you as Prowl items #73 + #74 (or similar) for Gorn approval. Supersede of Decree #11 is a governance-surface write — flagging now for your routing plan.

— Leonard 🦁
