# dep-upgrade-plan revision report

Bounty #53 was returned because the original skill planned upgrades from hand-supplied toy advisory data. This revision changes the skill so it actually gathers dependency evidence: it reads an npm package-lock, queries OSV.dev for exact locked package versions at run time, and emits a ranked package-level upgrade plan.

## Artifact map

- Registry listing: https://runx.ai/x/ryde-play/dep-upgrade-plan@sha-38180cef1396
- Source: https://github.com/RYDE-PLAY/runx/tree/fe0a77cf0bbb5f4e165d088513e75f8c711f01ac/skills/dep-upgrade-plan
- PR: https://github.com/runxhq/runx/pull/126
- Raw X.yaml: https://raw.githubusercontent.com/RYDE-PLAY/runx/fe0a77cf0bbb5f4e165d088513e75f8c711f01ac/skills/dep-upgrade-plan/X.yaml
- Raw SKILL.md: https://raw.githubusercontent.com/RYDE-PLAY/runx/fe0a77cf0bbb5f4e165d088513e75f8c711f01ac/skills/dep-upgrade-plan/SKILL.md
- Evidence JSON: https://raw.githubusercontent.com/RYDE-PLAY/frantic-53-dep-upgrade-plan/main/evidence.json
- Verification JSON: https://raw.githubusercontent.com/RYDE-PLAY/frantic-53-dep-upgrade-plan/main/verification.json
- Dogfood receipt JSON: https://raw.githubusercontent.com/RYDE-PLAY/frantic-53-dep-upgrade-plan/main/runx-receipt.json
- Receipt ref: `runx:receipt:sha256:4502f657b82c943d0aa3b1a3094e2c52891c0579ac1c852aaa3fa56d7aafafce`

## What changed

- The default path now queries OSV.dev `/v1/query` for each exact locked npm package version.
- The dogfood target is OWASP NodeGoat at commit `c5cb68a7084e4ae7dcc60e6a98768720a81841e8`, using its public package-lock URL.
- The plan aggregates multiple advisories into one target upgrade per package instead of producing duplicate one-advisory rows.
- The hosted registry harness is deterministic so publish does not depend on external network availability, while the post-publish dogfood proves the live OSV path.
- The old Fixture Shop toy lockfile and hand-authored advisory fixture were removed.

## Verification summary

- `runx skill inspect`: passed for version 0.2.0.
- Local harness: passed sealed and all-upgrades-blocked refusal cases.
- Upstream skill binding check: passed.
- Registry publish: published `ryde-play/dep-upgrade-plan@sha-38180cef1396`.
- Registry read/install: passed from `https://api.runx.ai`.
- Post-publish dogfood: live OSV mode found 13 advisory records across 16 direct production dependencies and produced 5 package upgrades.
- `runx verify`: valid production signature for receipt `sha256:4502f657b82c943d0aa3b1a3094e2c52891c0579ac1c852aaa3fa56d7aafafce`.

## Dogfood result

- underscore: 1.9.1 -> 1.13.8; risk=high; advisories=GHSA-cf4h-3jhx-xvhq, GHSA-qpx9-hpmf-5gmw
- body-parser: 1.18.3 -> 1.20.3; risk=high; advisories=GHSA-qwcr-r2fm-qrc7
- marked: 0.3.5 -> 4.0.10; risk=high; advisories=GHSA-5v2h-r2cx-5xgj, GHSA-7px7-7xjx-hxm8, GHSA-p9wx-2529-fp83, GHSA-rrrm-qjm4-v8hf, GHSA-vfvf-mqq8-rwqc, GHSA-x5pg-88wf-qq4p
- mongodb: 2.2.36 -> 3.1.13; risk=high; advisories=GHSA-mh5c-679w-hh4r
- express: 4.16.4 -> 4.20.0; risk=medium; advisories=GHSA-qw6h-vgh9-j6wx, GHSA-rv95-896h-c2vc

Refused candidates: swig: OSV advisory has no fixed npm version.
