# CLI Install Skill

## Problem Statement

**How might we ensure that after `/plugin install ingitdb@sneat-co`, the very next `/ingitdb:*` invocation succeeds — without making the plugin itself own multi-platform binary distribution?**

The plugin README declares the `ingitdb` CLI a prerequisite, but nothing in the plugin surface helps the user cross that gap. A human runs `/plugin install`, invokes a skill, and gets `command not found: ingitdb` with no in-context path forward.

## Recommended Direction

Ship a single skill — `/ingitdb:install` — that points the user at the platform-appropriate package manager command (Homebrew, WinGet, Snap, etc.) or the `go install` path. Every other skill in the plugin performs a pre-flight `command -v ingitdb` check; on miss, it emits a single error that references both paths (invoke the install skill, or run the install command manually). Reject bundling binaries, reject a SessionStart hook, reject a long-lived "doctor" skill.

This direction leans on assets the project already has: (1) the inGitDB project already publishes to Homebrew, Snap, AUR, WinGet, Chocolatey, Scoop, and the Go module proxy — the plugin does not re-solve multi-platform; (2) Claude Code's existing Bash permission prompt *is* the consent UI when an agent does execute the installer (with explicit user direction) — we do not invent a new one.

The pattern is shared with the sibling [`specscore`](https://github.com/synchestra-io/ai-plugin-specscore) and [`synchestra`](https://github.com/synchestra-io/ai-plugin-synchestra) plugins. The install skill is essentially a template with the CLI name and install commands swapped. Changes to one should be considered for the others.

## Explicit Non-goals

- **No bundled binaries.** The plugin ships skills (text), not executables.
- **No `curl … | sh` from inside the skill.** That's a trust decision belonging to the user, in their own terminal.
- **No SessionStart hook auto-installer.** Surprise installs at session start violate user expectation.
- **No long-lived "doctor" skill.** A single install pointer plus per-skill pre-flight checks covers the failure mode.
