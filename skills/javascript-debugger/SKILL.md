---
name: javascript-debugger
description: Diagnose and fix JavaScript bugs in Minecraft Bedrock add-ons and Script API code. Use when investigating errors, unexpected behavior, or failing scripts.
---

# JavaScript Debugger

Find the root cause from evidence. Recommend the smallest safe fix.

## Diagnostic workflow

1. Collect the full error, stack trace, reproduction steps, Minecraft version, module versions, and relevant code.
2. Trace the data flow and event lifecycle. Separate syntax errors, runtime errors, API compatibility issues, and logic bugs.
3. Check `undefined` and `null`, types, world/entity assumptions, timing, event registration, and asynchronous operations.
4. Verify suspected APIs for the target version. Do not assume availability based on examples from another version.
5. Fix the cause, not just the visible error. Keep the change as small as practical.
6. Provide reproduction, log-check, and regression-test steps.

## Data safety

- Do not delete or reset dynamic properties or player data to hide a symptom.
- Do not swallow errors without clear logging or handling.
- Preserve existing identifiers and behavior unless a change is required and includes a migration plan.

## Error handling

- State what is known from logs and what is only a hypothesis.
- If evidence is insufficient, request the missing reproduction details.
- Do not claim a fix is verified unless it was tested.

## Testing checklist

- [ ] The issue has clear reproduction steps.
- [ ] The first relevant error and source location were identified.
- [ ] Suspected APIs were checked against the target version.
- [ ] The proposed fix addresses the root cause and preserves data.
- [ ] Regression steps cover the original failure and relevant edge cases.
- [ ] Test results distinguish static review from runtime testing.

## Response format

Report the root cause, supporting evidence, file/line, proposed fix, and verification steps. If the cause is uncertain, label it as a hypothesis and ask for details needed to confirm it.
