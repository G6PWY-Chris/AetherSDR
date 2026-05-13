# WHISKEY ABSOLUTE RULES
## Read this before doing ANYTHING else. No exceptions. Applies to every project.
1. Every instruction, decision, fact, or preference the user states → written to disk BEFORE the next response. Not at commit time. Not at the end. IMMEDIATELY. When in doubt — SAVE IT. Lost context has cost the user 3+ days of repeated work.
2. Every session start — read `.claude/RESUME.md` then run `git status` — commit and push anything uncommitted before starting new work.
3. Every commit → `git push` immediately. GitHub is the backup. Do not accumulate commits.
4. Use Ollama instead of Claude API wherever possible. Every Claude Pro token costs money. All software: open source, self-hosted, zero cost — no exceptions.
5. Firewalls, switches, DNS, network config: NO changes without explicit user sign-off first. Stop and ask. No exceptions. Not even "small" changes.
6. `.claude/RESUME.md` is a live document — keep it current at all times. When compact is needed: update RESUME.md → commit and push → user types /compact. Never compact first.
7. Always use the Read tool on a file before the Edit tool — even if you just grepped it. Skipping this causes a confusing error message that is off-putting to the user.
8. Every session start — run the session monitor in the background: `bash ~/github/Projects-Claude/Homelab/scripts/session-monitor.sh`
9. Document as we go — update research files, RESUME.md, and memory files during the session, not just at the end.
10. **GOLDEN RULE — SSH before internet:** Before doing ANY web browsing, GitHub API calls, or external network research, SSH to ubuntu01 first: `ssh claude@192.168.40.11`. This is Claude's own account. ubuntu01 is the PRIMARY machine for scripts and research. Foxtrot (192.168.40.101, chris account) is the fallback. dev=192.168.40.100 is this machine. Run `gh`, `curl`, or `wget` remotely. Only fall back to local WebFetch/WebSearch if neither host responds.
