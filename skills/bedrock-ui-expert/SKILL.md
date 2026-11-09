---
name: bedrock-ui-expert
description: Design Minecraft Bedrock form UI with Action Forms, Modal Forms, Message Forms, and player interaction state. Use for menus, form validation, and `@minecraft/server-ui` compatibility.
---

# Bedrock UI Expert

Design and review Bedrock form flows with version checks, safe player state, and clear input validation.

## Responsibilities

- Action Form, Modal Form, and Message Form design.
- Player interaction logic and UI state transitions.
- Input validation, cancellation handling, and recovery flows.
- Menus, settings, confirmation flows, and player choices.
- `@minecraft/server-ui` compatibility checks.

## Technical rules

- Verify form APIs against the target Bedrock version and declared module dependency.
- Do not assume `@minecraft/server-ui` behaves the same across versions.
- Keep UI state separate from persistent world state. A form response does not prove that a data change succeeded.
- Validate input before changing dynamic properties, progression, economy, or inventory state.
- Preserve player data when a form is dismissed or canceled.
- Use `bedrock-api-expert` for general API verification. Focus this skill on UI flow and response handling.

## Workflow

1. Identify the player's goal, form type, and target Bedrock version.
2. Verify the required module dependency and API behavior in official documentation for that version.
3. Define the UI state: current screen, choices, and data needed until submission.
4. Build the form content around safe input and clear choices.
5. Validate the response before changing player or world state.
6. Handle cancellation, invalid selections, and stale state.
7. Test success, cancellation, invalid input, and multiplayer behavior when the runtime is available.

## Error handling

- Do not apply destructive changes if the form is closed or canceled.
- Reject missing or malformed response data. Reopen the form only when appropriate.
- If callbacks or event order differ, check lifecycle and timing assumptions.
- State when a UI issue depends on a specific version. Give conditional guidance when needed.
- Report exact errors and separate documented behavior from hypotheses.

## Testing checklist

- [ ] Test each form flow on the target version when possible.
- [ ] Check cancel, close, and invalid input paths.
- [ ] Confirm selections and labels remain consistent after updates.
- [ ] Check event order and state cleanup.
- [ ] Confirm form errors do not lose player data.
- [ ] Do not claim runtime testing if it was not performed.

## Compatibility and references

Distinguish stable APIs from beta or experimental requirements using the module documentation. Check the `@minecraft/server-ui` dependency in `manifest.json`. Do not apply preview examples to a stable runtime without verification. See the [repository versioning guide](../../docs/bedrock-api-versioning.md) and official [`@minecraft/server-ui` reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server-ui/minecraft-server-ui?view=minecraft-bedrock-stable).

Report the UI design, version assumptions, data flow, validation rules, and test plan. State uncertainty and suggest a verified fallback when API support is unclear.
