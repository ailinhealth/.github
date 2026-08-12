# ailinhealth/.github

Org-wide GitHub **defaults**: the reusable workflows every repo calls, and the
default pull request template.

Declarative org configuration — labels, rulesets, the repo inventory — lives in
the private **[ailinhealth/platform-config](https://github.com/ailinhealth/platform-config)**
repo, not here.

## ⚠️ This repository is PUBLIC, and must stay public

GitHub does not serve default community health files from a private `.github`
repo, and pull request templates specifically require **public** — an internal
repo will silently fail to apply them. If this repo is made private the PR
template stops applying org-wide with no error.

Consequences to keep in mind:

- **Everything here is world-readable.** Never add secrets, tokens, internal
  hostnames, customer names, regulatory classifications, or anything about the
  system architecture that isn't already public.
- **Anyone can call these reusable workflows.** Harmless — they'd run on the
  caller's own runners — but it means these workflows must never accept or
  reference secrets.
- Anything sensitive goes in `platform-config` instead.

## ⚠️ Changes here are live for every repository at once

The reusable workflows are consumed as `@main`:

```yaml
uses: ailinhealth/.github/.github/workflows/quality-gate.yml@main
```

**Any push to `main` takes effect immediately in every repository**, whether or
not it has migrated to the v2 branching model.

The `model` input on `branch-flow.yml` exists for exactly this reason. It
defaults to `v1` (the legacy `dev → pre → main` chain), so repos are unaffected
until they opt in by passing `model: "v2"` in their own caller workflow — a
reviewed PR in that repo, part of its migration.

**Never change v1 behaviour while any repo still depends on it.** See
`config/repos.yml` in `platform-config` for who is still on it.

## Contents

```
.github/
  pull_request_template.md   Org default. Applies to any repo without its own
  workflows/
    branch-flow.yml          Reusable. v1/v2 branch policy
    quality-gate.yml         Reusable. Lint, static analysis, tests, build
    pr-labels.yml            Reusable. Exactly one type label
    pr-title.yml             Reusable. type(scope): description [TICKET-123]
```

## Merge queue

These are `workflow_call` workflows, so they have no triggers of their own.
**The `merge_group:` trigger goes on the caller** in each repo. Without it the
check never runs in the merge group and the queue waits indefinitely with no
error.

The PR-level checks (`branch-flow`, `pr-labels`, `pr-title`) return early and
pass on `merge_group` events, since they were already enforced on the pull
request that produced the merge group. That lets them stay in the required
status checks list without stalling the queue.

## What cannot be centralised here

`release.yml` (changelog config), `CODEOWNERS`, and `dependabot.yml` are **not**
supported as org default community health files. Every repo keeps its own copy.
`platform-config/config/canonical/` holds the reference versions and the config
sync reports drift; fixing it is a PR in the affected repo.

## Before merging changes here

- [ ] Nothing sensitive added — this repo is public
- [ ] Does this alter v1 behaviour? If so, stop and check `repos.yml`
- [ ] Tested by pointing one caller at your branch (`@your-branch`) and opening
      a throwaway PR, rather than by merging and hoping
- [ ] If a job name changed, `platform-config/config/rulesets/main.json`
      required status checks updated to match
