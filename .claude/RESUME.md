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

- **2026-05-17** — PR #2823 OPEN — feat(models): add RadioModel::autoSaveChanged signal, wire ProfileManagerDialog (issue #2794). Opus adversarial review: PASS, recommend merge as-is. Awaiting CI + Jeremy review.
- **2026-05-16** — PR #2642 MERGED ✓ — fix(gui): display TX timeout in seconds instead of milliseconds
- **2026-05-16** — Session start: rebased local main onto upstream/main (skipped already-merged 200a302).
- **2026-05-14** — Local build fixed: installed libssl-dev, CMake now uses system OpenSSL 3.0.13
- **2026-05-14** — git ship workflow fixed: two-step (ship + ship-pr), branches from upstream/main only

## PR status

- **PR #2823** — OPEN — feat(models): add RadioModel::autoSaveChanged signal (#2794)
- **PR #2642** — MERGED ✓ — fix(gui): display TX timeout in seconds instead of milliseconds

## git workflow — CORRECT PROCEDURE

1. `git fetch upstream && git checkout -b fix/<branch-name> upstream/main`
2. Make changes, `git commit -S -m "..."`
3. `git push -u origin fix/<branch-name>` then `gh pr create --repo ten9876/AetherSDR --base main --head chrisb1964:<branch>`
**NEVER commit fixes to local main — .claude/ metadata bleeds into PR diff**
**NOTE: `git ship` alias is broken in bash (syntax error with function defs)**

## CMake build (local) — always use these flags

```
cmake -B build -G Ninja -DCMAKE_BUILD_TYPE=RelWithDebInfo -DOPENSSL_ROOT_DIR=/usr -DOPENSSL_USE_STATIC_LIBS=OFF
```

Qt 6.11.1 build currently broken — Qt6Multimedia not found at expected path even with CMAKE_PREFIX_PATH set. CI Docker image works fine.

## Bug status (3 remaining)

1. **TGXL fwd power not resetting** — TunerModel.cpp never zeroes m_fwdPower on PTT release.
2. **PGXL power gauge not resetting** — AmpApplet::setState() doesn't zero gauge on TRANSMIT→IDLE.
3. **PGXL fan mode** — PgxlConnection.cpp has zero FAN commands. Full feature work needed.

## Next work

1. Pick next issue — top candidate: #2743 (DIGU squelch split, priority: high) — split combined squelch command to match FlexLib, ~6 caller sites
2. Use corrected git workflow above — NOT git ship alias
3. End-of-session: always run Opus adversarial review before declaring done (saved to memory)

## Build — Qt 6.11.1 (GPU spectrum enabled)

```bash
# From /home/chris/github/Projects-Claude/AetherSDR-git
cmake -B build -G Ninja \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DCMAKE_PREFIX_PATH="$HOME/Qt/6.11.1/gcc_64" \
  -DOPENSSL_ROOT_DIR=/usr \
  -DOPENSSL_USE_STATIC_LIBS=OFF
cmake --build build -j$(nproc)
```

Missing deps still needed before build:
```bash
sudo apt install -y libfftw3-dev portaudio19-dev libhidapi-dev qtkeychain-qt6-dev libxkbcommon-dev libopengl-dev
```

ENABLE_BNR (NVIDIA NIM) skipped — requires RTX 4000+ and grpc++. GTX 1080 Ti not supported.

## Key reminders

- Firmware **4.2.18**, version **CalVer 26.5.2.1** (updated upstream)
- Signed commits: `git commit -S`
- CI must pass, Jeremy reviews all src/ changes
- **GOLDEN RULE:** `ssh claude@192.168.40.11` before any internet research
