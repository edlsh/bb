---
name: acp-provider
description: "Configure or troubleshoot ACP agent discovery, custom models, skills, and compaction in BB."
---

# ACP providers

Known agents can be discovered automatically when their CLI is installed on the
host: `opencode`, `omp`, `grok`, and `hermes` appear as `acp-opencode`, `acp-omp`,
`acp-grok`, and `acp-hermes-agent`. Inspect the target host's catalog with
`bb provider list` and `bb provider models <provider-id>` using its environment
or machine selector.

ACP model catalogs expose the upstream model provider as `routeProviderId` in
`bb provider models <provider-id> --json` and the SDK's `AvailableModel` records.
The bridge preserves an explicit `routeProviderId` from ACP model entries;
otherwise it uses the first segment of a `provider/model` ID. Nested IDs such as
`openrouter/anthropic/claude-sonnet-5` belong to `openrouter`. Bare IDs and agent
defaults have no inferred provider. Model selection still uses the complete
`model` value; the provider field is catalog metadata.

Cursor project skills come from `.cursor/skills`, which can link to
`.agents/skills`. BB lists these linked skills as read-only under `cursor-project`.

ACP agents may reject unlisted model IDs. OpenCode requires models in its own
configuration; BB discovers them there. OpenCode agents are session modes, not
models selectable through BB's model field.

OpenCode ACP supports the core `bb thread compact` command; Cursor ACP does not
expose compatible compaction. Check the actual agent's capabilities before
attempting provider-specific recovery.
