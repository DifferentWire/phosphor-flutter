# phosphor-flutter (DifferentWire fork) — CLAUDE.md

> **Standards:** This repo follows DifferentWire standards.
> Read and apply: `C:\Dev\DifferentWire\standards\CLAUDE-BASE.md`, `C:\Dev\DifferentWire\standards\SAFELANE.md`

## What this is

A **fork** of [`phosphor-icons/phosphor-flutter`](https://github.com/phosphor-icons/phosphor-flutter) (MIT), maintained only to carry a compatibility patch that upstream has not yet shipped. **This is not a greenfield DifferentWire project** — it is a vendored fork consumed as a git dependency by DW Flutter apps.

See [`FORK.md`](./FORK.md) for the patch, the reason, and the retirement plan.

## Project Parameters

| Field | Value |
|-------|-------|
| Repository | https://github.com/DifferentWire/phosphor-flutter |
| Upstream | https://github.com/phosphor-icons/phosphor-flutter (MIT) |
| Citadel project | phosphor-flutter (relaxed: no-issue-link — asset/fork repo) |
| Consumed by | DifferentWire/Unfocused (git dep on `main`); MeshCore projects may adopt |
| BUILD_COMMAND | `dart analyze lib/` (build against Flutter ≥3.44) |

## Working rules

- **Minimize divergence from upstream.** Only the compatibility patch lives here. Do not add features, refactor, or reformat — every extra change makes the eventual upstream retirement harder.
- **Track upstream.** When upstream ships a Flutter-3.44-compatible release, this fork retires: point consumers back at pub.dev and archive the repo.
- **Push the fix upstream.** The patch should be offered to upstream as a PR so the fork can die.
- Governance (Citadel task before commits, worktrees, tollgates) per SAFELANE / CLAUDE-BASE. Issue-link is relaxed for this asset repo.
