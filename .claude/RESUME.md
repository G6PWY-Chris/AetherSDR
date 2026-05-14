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

- **2026-05-14** — PR #2642 opened: fix(gui) TOT display in minutes not ms (Fixes #2617). Screenshot attached. Awaiting CI + Jeremy.
- **2026-05-14** — Local build fixed: installed libssl-dev, CMake now uses system OpenSSL 3.0.13
- **2026-05-14** — git ship workflow fixed: two-step (ship + ship-pr), branches from upstream/main only

## PR status

- **PR #2642** — OPEN — fix(gui): display TX timeout in minutes instead of milliseconds

## git workflow — CORRECT PROCEDURE

1. `git ship fix/<branch-name>` — creates clean branch from upstream/main, switches to it
2. Make changes, `git commit -S -m "..."`
3. `git ship-pr` — pushes to fork, opens PR
**NEVER commit fixes to local main — .claude/ metadata bleeds into PR diff**

## CMake build (local) — always use these flags

```
cmake -B build -G Ninja -DCMAKE_BUILD_TYPE=RelWithDebInfo -DOPENSSL_ROOT_DIR=/usr -DOPENSSL_USE_STATIC_LIBS=OFF
```

## Bug status (3 remaining)

1. **TGXL fwd power not resetting** — TunerModel.cpp never zeroes m_fwdPower on PTT release.
2. **PGXL power gauge not resetting** — AmpApplet::setState() doesn't zero gauge on TRANSMIT→IDLE.
3. **PGXL fan mode** — PgxlConnection.cpp has zero FAN commands. Full feature work needed.

## Next work

1. Wait for PR #2642 CI + review
2. Pick next issue: #2445 (filter buttons not highlighting) or #2393 (PGXL power erratic)
3. Use correct git ship workflow — branch from upstream/main first

## Key reminders

- Firmware **4.2.18**, version **CalVer 26.5.1**
- Signed commits: `git commit -S`
- CI must pass, Jeremy reviews all src/ changes
- **GOLDEN RULE:** `ssh claude@192.168.40.11` before any internet research
