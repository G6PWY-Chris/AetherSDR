---
name: AetherSDR Project State
description: Current contribution status, last merged PR, open work
type: project
---
## Contribution Status

- **Fork:** chrisb1964/AetherSDR (remote: `origin`)
- **Upstream:** ten9876/AetherSDR (remote: `upstream`)
- **Current version:** 26.5.1 (CalVer — switched from semver at v0.9.8)
- **Fork synced:** 2026-05-14 (merged upstream/main through commit ca62065)

## Last Merged PR

- **PR #2250** — "Fix TGXL presence when detected via direct TCP only (Fixes #2174)"
- **Commit:** 8c856e3
- **Status:** Merged to upstream main ✅

## Known Bugs — Status as of 2026-05-14

See `.claude/research/aethersdr-bug-audit.md` for full details.

1. **TGXL forward power not resetting after TX ends** — `m_fwdPower` in TunerModel.cpp is never zeroed when pttA drops. No PTT state handling in TunerModel at all. STILL EXISTS.
2. **PGXL power gauge not resetting after TX ends** — AmpApplet::setState() changes button label/color but does not zero the Fwd Power gauge. Partial fix #2437 (OPERATE/STANDBY sync) landed but did NOT fix power reset. STILL EXISTS.
3. **PGXL fan mode buttons** — PgxlConnection.cpp has NO FAN commands at all (only 149 lines). UI not implemented. STILL EXISTS.
4. **EFF/meffa label** — FIXED by #2444 (`fix(amp): forward radio amplifier telemetry to AmpApplet`). AmpApplet::setMeff() now shows "MEffA: {value}" label correctly.

## Firmware Version Update

- Reference radio now on **fw 4.2.18** (was 4.1.5 in old CLAUDE.md — updated upstream)

## Contribution Opportunities

See `.claude/research/aethersdr-contribution-opportunities.md` — 12 candidate issues mapped, 9 easy/medium complexity.

## CI/CD

- Docker image: `ghcr.io/ten9876/aethersdr-ci:latest` (~3.5 min builds)
- Signed commits required on main
- `git ship` alias for PR workflow
- CODEOWNERS review required (Jeremy/KK7GWY)
