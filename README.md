# skills4sofia

Skill source repository for Sofia.

This repository is the development and release source of Agent skills. The HarmonyOS app keeps a bundled fallback snapshot so Sofia can still work offline or when cloud delivery is unavailable.

## Layout

```text
catalog.json
skills/
  sofia-phone-operation/SKILL.md
  sofia-failure-recovery/SKILL.md
  sofia-price-comparison/SKILL.md
  sofia-jd/SKILL.md
  sofia-taobao/SKILL.md
  sofia-pinduoduo/SKILL.md
  sofia-wechat/SKILL.md
  sofia-result-presentation/SKILL.md
```

## Runtime model

Sofia does not require skill content to be compiled into the Agent loop. The runtime reads a catalog, selects only the skills relevant to the current task, and loads their content through a `SkillSource` abstraction.

Today:

```text
SofiaSkillRegistry
  -> BundledSkillSource
  -> HAP fallback snapshot
```

Target cloud path:

```text
Remote Config
  -> selects catalog/release/rollout
Cloud Storage
  -> stores catalog + SKILL.md artifacts
SofiaSkillRegistry
  -> CloudSkillSource
  -> verified local cache
  -> bundled fallback on failure
```

The Agent loop should not care whether a skill came from the HAP, a downloaded cache, or a future cloud source.

## catalog.json

Each skill entry contains:

- `name`: stable skill identifier.
- `version`: skill semantic version.
- `enabled`: release switch.
- `layer`: core, task, app, presentation, etc.
- `priority`: prompt ordering.
- `artifact`: repository/cloud artifact path.
- `sha256`: content integrity hash.
- `activation`: when the skill is selected.

Activation modes currently supported by Sofia:

- `always`: always load.
- `keywords`: load when the task contains any configured keyword.
- `app`: load when an app alias is in the task or a discovered bundle matches.
- `any`: keyword/app match.

Example future app skill:

```json
{
  "name": "sofia-jd",
  "version": "1.0.0",
  "enabled": true,
  "layer": "app",
  "priority": 50,
  "artifact": "skills/sofia-jd/SKILL.md",
  "sha256": "...",
  "activation": {
    "mode": "app",
    "any": [],
    "appAliases": ["京东", "JD"],
    "bundles": ["com.jd.hm.mall"]
  }
}
```

## Release direction

GitHub is the source of truth for development, review, history and tagging. A later publish workflow can upload immutable skill artifacts to Huawei Cloud Storage and publish a release pointer through Remote Config. Remote Config can then control enablement, version selection and staged rollout without an AppGallery app update.

Cloud-delivered content should be downloaded to app-private storage, verified against the expected SHA-256, activated atomically, and rolled back to the previous verified catalog or bundled snapshot on failure.

## Current snapshot (2026-10-02)

Catalog `2026-10-02.2` contains eight skills and matches the bundled snapshot in Sofia 1.9.34. Native Agent discovery exposes catalog metadata first and reads selected content through `harmony_skill_read`.

The current app still loads its bundled snapshot. Publishing this repository does not automatically update installed apps; a remote skill downloader and verified cache are not implemented yet. The Linux Codex path still installs four core skills from the app package.

Recent updates cover saved-login reuse, shopping without per-app call quotas, controller approval and manual takeover, file and original gallery photo delivery, and embedded-browser routing.

WeChat guidance covers conversation replies, Moments drafts, informational sheets, Sofia window occlusion and final-step Send/Publish approval. Native Agent also loads the matching app Skill when opening its exact bundle.
