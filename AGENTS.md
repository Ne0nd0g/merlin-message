# AGENTS.md — merlin-message

Guidance for AI coding agents working in this repo. Human contributors may find it useful too.

## What this is

The **shared message protocol** for Merlin — the small library that defines the structs exchanged
between the server and agents (base messages, jobs, OPAQUE auth, RSA). Go module
`github.com/Ne0nd0g/merlin-message`. It sits at the **base of the dependency chain**: it is imported
by the server, the agent, the agent DLL, and the Mythic container.

Target Go: **1.27**. Dependencies are intentionally minimal (currently just `github.com/google/uuid`).

## Build / test

```bash
go build ./...
go vet ./...
go test ./...
```

Packages: the root package plus `jobs/`, `opaque/`, `rsa/`. (No unit tests yet — additions welcome.)

## Why changes here are high-impact

Because every other Merlin repo imports this module, a change to the wire structs ripples across the
whole project. Treat the message format as a compatibility contract:
- Prefer additive changes; avoid renaming/removing fields without a coordinated bump everywhere.
- After tagging a new version, bump the `require` in each dependent (server, agent, agent-dll, mythic
  container) and re-validate — see the release runbook and `revival-plan.md`.

## Conventions

- **Branches:** do all work on `dev` (or a feature branch). **Never commit to `main`.**
- **Commits:** the maintainer signs every commit with a YubiKey. **Do not run `git commit`** —
  stage changes and propose a commit message. Do **not** add a `Co-Authored-By` trailer.
- Match surrounding style; keep the GPLv3 license header on new Go files.
