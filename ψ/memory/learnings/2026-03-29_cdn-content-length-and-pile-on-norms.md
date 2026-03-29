# Lesson: CDN Content-Length Headers & Governance Enforcement

**Date**: 2026-03-29
**Source**: Day 13 Session 1

## CDN Content-Length

When serving static files through a CDN (Cloudflare), the content-length header must be set correctly. Hono's `c.body()` with a Node Buffer sends content-length: 0 even though the response body is correct. CDNs trust the header and may cache empty content, causing users to receive broken pages.

Fix: explicitly set `Content-Length: buffer.length` before calling `c.body()`.

## Governance Norms Need Teeth

Soft norms (SHOULD) that rely on cultural adoption don't stick under pressure. When multiple Beasts receive the same stimulus (e.g., Gorn asking a question), they all respond simultaneously without checking if someone already answered. The pile-on norm was discussed, acknowledged, and violated again within 15 minutes — twice.

Options: upgrade to decree (MUST), add tooling enforcement (rate-limit responses per thread), or accept it as a cost of parallelism.

## Secretary Pattern Scales

The DM→forum→task→build→review→notify pipeline handled 35+ tasks without collisions. Key: one router (Leonard), one tasker (Zaghnal), builders assigned per task, reviewers per task. No ambiguity about who does what.
