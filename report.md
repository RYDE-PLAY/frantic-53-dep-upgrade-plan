# dep-upgrade-plan delivery report

Bounty #53 requested a published runx skill named `dep-upgrade-plan` that produces a dependency upgrade plan from advisory facts and constraints. The delivered package is `ryde-play/dep-upgrade-plan@sha-7a1f34b0`, sourced from PR #126 at commit `7a1f34b0c878988a46a4fadb493f9079a08a042e`.

## Artifact map

- Registry listing: https://runx.ai/x/ryde-play/dep-upgrade-plan@sha-7a1f34b0
- Source: https://github.com/RYDE-PLAY/runx/tree/7a1f34b0c878988a46a4fadb493f9079a08a042e/skills/dep-upgrade-plan
- PR: https://github.com/runxhq/runx/pull/126
- Raw X.yaml: https://raw.githubusercontent.com/RYDE-PLAY/runx/7a1f34b0c878988a46a4fadb493f9079a08a042e/skills/dep-upgrade-plan/X.yaml
- Raw SKILL.md: https://raw.githubusercontent.com/RYDE-PLAY/runx/7a1f34b0c878988a46a4fadb493f9079a08a042e/skills/dep-upgrade-plan/SKILL.md
- Evidence JSON: https://raw.githubusercontent.com/RYDE-PLAY/frantic-53-dep-upgrade-plan/main/evidence.json
- Verification JSON: https://raw.githubusercontent.com/RYDE-PLAY/frantic-53-dep-upgrade-plan/main/verification.json
- Dogfood receipt: https://raw.githubusercontent.com/RYDE-PLAY/frantic-53-dep-upgrade-plan/main/runx-receipt.json

## What the skill does

The skill reads a package lock, advisory records, and release constraints. It emits `dep.upgrade.plan.v1` with ranked `plan[{pkg,from,to,risk,breaking}]`, changelog entries, and refused candidates. It does not install packages, mutate manifests, run target project code, or open dependency PRs.

## Verification summary

- `runx skill inspect`: passed.
- Local harness: passed with one sealed ranked-plan case and one all-upgrades-blocked refusal case.
- Upstream skill binding check: passed.
- Registry publish: published `ryde-play/dep-upgrade-plan@sha-7a1f34b0`.
- Registry read: returned the expected skill id, owner, version, and digest.
- Registry install: installed from the remote registry with community trust tier.
- Post-publish dogfood: sealed receipt `sha256:f11a5df5a43144c288215d512db078cf69d3bb6c1c349e8412e4cc99c9194e73`.
- `runx verify`: valid production signature, valid digest, valid content address.

## Dogfood result

The dogfood run produced 2 upgrade recommendations: `lodash 4.17.19 -> 4.17.21`, `express 4.16.4 -> 4.20.0`. It also refused 1 blocked candidate: `debug 2.6.8 -> 4.3.1`.
