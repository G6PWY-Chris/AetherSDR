# RESUME — AetherSDR Project

# WHISKEY ABSOLUTE RULES READ AND REMEMBER
## Read this before doing ANYTHING else. No exceptions. Applies to every project.
1. Every instruction, decision, fact, or preference the user states → written to disk BEFORE the next response. Not at commit time. Not at the end. IMMEDIATELY. When in doubt — SAVE IT. Lost context has cost the user 3+ days of repeated work.
2. Every session start — read `.claude/RESUME.md` then run `git status` — commit and push anything uncommitted before starting new work.
3. Every commit → `git push` immediately. GitHub is the backup. Do not accumulate commits.
4. Use Ollama instead of Claude API wherever possible. Every Claude Pro token costs money. All software: open source, self-hosted, zero cost — no exceptions.
5. Firewalls, switches, DNS, network config: NO changes without explicit user sign-off first. Stop and ask. No exceptions. Not even "small" changes.
6. `.claude/RESUME.md` is a live document — keep it current at all times. When compact is needed: update RESUME.md → commit and push → user types /compact. Never compact first.
7. Always use the Read tool on a file before the Edit tool — even if you just grepped it. Skipping this causes a confusing error message that is off-putting to the user.
8. Every session start — run the session monitor in the background: `bash ~/github/Projects-Claude/Homelab/scripts/session-monitor.sh`
9. Chris has health conditions that affect memory. Document EVERYTHING as we go — decisions, fixes, configs, and the WHY behind them. RESUME.md must always reflect current state. Disaster recovery is a top priority: every service needs a clear recovery path written down so the cluster can be rebuilt without relying on memory.
## Last completed work

- **2026-05-14** — Synced fork: merged upstream/main (ca62065) into chrisb1964/AetherSDR. 154 files changed, project now at v26.5.1 (CalVer).
- **Bug audit updated** — Bug #4 (meffa label) FIXED upstream by #2444. Bugs 1–3 still open.
- **Golden Rule added** — Rule 10: SSH to dev/ubuntu01/foxtrot before any internet research.

## Bug status (3 remaining)

1. **TGXL fwd power not resetting** — TunerModel.cpp never zeroes m_fwdPower on PTT release. No pttA handling at all. Candidate for our next PR.
2. **PGXL power gauge not resetting** — AmpApplet::setState() doesn't zero the gauge on TRANSMIT→IDLE. #2437 fixed button only.
3. **PGXL fan mode** — PgxlConnection.cpp has zero FAN commands. Full feature work needed.

## Next work

1. SSH to dev/ubuntu01/foxtrot (check which is up) before doing any GitHub research
2. File GitHub issue for Bug 1 (TGXL fwd power reset) — clearest bug, most likely to be accepted
3. Implement fix in TunerModel.cpp, test with live TGXL, use `git ship` to open PR

## Key reminders

- Firmware now **4.2.18** (was 4.1.5) — update any protocol comments
- Version now **CalVer 26.5.1** (not semver)
- Signed commits required: `git commit -S`
- CI must pass before PR is mergeable
- Read CONTRIBUTING.md before any change
- Jeremy (KK7GWY) is the maintainer — design decisions need his review
- **GOLDEN RULE:** SSH to dev/ubuntu01/foxtrot before going onto the internet
