# Bedrock API versioning guide

Minecraft Bedrock versions change quickly. Many features that appear valid in one version are not supported or behave differently in another. This project treats API compatibility as a first-class requirement.

## Core rules

1. Always confirm the target Minecraft Bedrock version before suggesting or using an API.
2. Check the matching module version and engine requirement in the pack manifest.
3. Distinguish stable APIs from beta, experimental, or preview features.
4. Do not assume an API works because it exists in a similar example elsewhere.
5. When uncertainty remains, mark the choice as version-dependent and ask for the target version or provide conditional options.

## What to verify

Before using a Script API or feature, confirm:

- the Bedrock engine version
- the module version in `manifest.json`
- whether the feature requires experimental toggles
- whether the same API name or behavior is available in all target versions
- whether the feature is supported in both client and server contexts where needed

## Safety principles

- Keep behavior valid for the lowest supported version in the pack, unless multiple versions are explicitly supported.
- Preserve existing identifiers, UUIDs, and dynamic properties.
- Avoid proposing features that need brittle version-conditional code paths without clear documentation or evidence.
- When a feature is only supported in newer versions, state that clearly and propose a fallback or phased rollout.

## Example workflow

1. Identify the target version.
2. Review the current pack manifest and modules.
3. Check whether the API is documented for that exact version.
4. Confirm if the feature is stable or experimental.
5. Implement only if compatibility is confirmed or the behavior remains explicitly conditional.
6. Validate with the target engine version in a test world.

## Common pitfalls

- Reusing API examples from a different version.
- Assuming UI APIs are available in every script setup.
- Mixing stable APIs with preview-only features.
- Ignoring the difference between a script module version and the Bedrock engine version.
- Changing identifiers without migration planning.

## Documentation references

- Official Minecraft Bedrock documentation
- Microsoft Learn references for Bedrock scripting and pack structure
- Current project skill files in `skills/`

Related docs:
- [Architecture overview](./architecture.md)
- [Skill development guide](./skill-development-guide.md)
- [Troubleshooting guide](./troubleshooting.md)
