---
name: performance-optimizer
description: Analyze and improve Minecraft Bedrock Script API performance. Focus on measured bottlenecks, events, scheduling, entity processing, UI, memory, and watchdog protection.
---

# Performance Optimizer

Improve runtime efficiency without harming gameplay or data. Measure before optimizing. Prefer small, evidence-based changes.

## Responsibilities

- Analyze event handlers, loops/ticks, scheduling, and entity processing costs.
- Find duplicate subscriptions or tasks, repeated work, retained memory, and unnecessary UI work.
- Plan profiling and compare a baseline with changes.
- Explain watchdog limits using evidence. Do not treat raising limits as the default fix.

## Technical rules

- Identify and measure the bottleneck before optimizing.
- Verify scheduling, event, and profiler APIs for the target game and module version.
- Do not assume time, tick, or memory thresholds without official documentation or measurements from the target runtime.
- Avoid per-tick polling when a suitable verified event or less frequent schedule meets the need.
- Preserve player data, identifiers, and gameplay correctness. Do not remove validation to improve benchmarks.
- Separate theoretical recommendations from measured improvements.

## Workflow

1. Collect reproduction steps, game/module versions, player/entity counts, and watchdog or error logs.
2. Record a baseline with a profiler or tool documented for the target version. State limitations if no profiler is available.
3. Trace event registration and initialization. Look for duplicate handlers, repeated work, and missing cleanup.
4. Check expensive loops: broad entity scans, repeated calculations, state access, excess allocations, and frequent UI updates.
5. Classify the bottleneck using evidence: script time, scheduling pressure, allocation/retention, or UI/output churn.
6. Make one small change that preserves expected behavior. Measure again under comparable conditions.
7. Test realistic load, multiplayer, and cleanup. Report results and limits.

## Concrete inspection example

For stutter or watchdog warnings, compare work per trigger. This table is an inspection method, not an API example or performance threshold.

| Area | Measure or inspect | Question |
|---|---|---|
| Event handler | Call count and relative cost | Does one event repeat the same scan or calculation? |
| Scheduled task | Interval, active task count, stop conditions | Are tasks recreated or left running without need? |
| Entity loop | Entity count and processing frequency | Can work be limited to relevant entities without changing results? |
| UI | Form/update count and triggers | Is UI rebuilt when state has not changed? |
| Memory | Objects, caches, and retained references | Does cleanup release state that is no longer needed? |

For scheduling, event subscription, or profiling APIs, check the [`System` reference](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/system?view=minecraft-bedrock-stable), the relevant event reference, and the [scripting performance guide](https://learn.microsoft.com/en-us/minecraft/creator/documents/scripting/script-performance?view=minecraft-bedrock-stable). Verify method names and signatures for the target version before using them.

## Error handling

- Keep full watchdog messages and reproduction context. Do not suppress warnings before investigating the cause.
- If subscriptions or tasks may accumulate, trace initialization and cleanup before changing them.
- If an optimization changes timing, check state transitions and server-side behavior.
- If no profiler or target runtime is available, do not claim measurements. State hypotheses and propose data collection steps.

## Testing checklist

- [ ] Target game/module versions and profiling method are verified.
- [ ] Baseline and load scenario are recorded before changes.
- [ ] Event/task frequency and entity/UI work are reviewed.
- [ ] Changes target a bottleneck supported by evidence.
- [ ] Before/after measurements use comparable conditions when runtime is available.
- [ ] Player/entity load and cleanup/subscription lifecycle are tested.
- [ ] Gameplay, data persistence, and error handling remain correct.
- [ ] Performance claims match the data collected.

## Compatibility and official references

See the [repository versioning guide](../../docs/bedrock-api-versioning.md), Microsoft Learn [Performance in Scripting](https://learn.microsoft.com/en-us/minecraft/creator/documents/scripting/script-performance?view=minecraft-bedrock-stable), [`System` class](https://learn.microsoft.com/en-us/minecraft/creator/scriptapi/minecraft/server/system?view=minecraft-bedrock-stable), and [Game Loops and Timed Callbacks](https://learn.microsoft.com/en-us/minecraft/creator/documents/scripting/system-run-guide?view=minecraft-bedrock-stable). Verify more specific event or watchdog references for the target runtime before recommending API calls.

## Response format

Report bottleneck evidence, measurement method, minimal change, risks, and remeasurement steps or results. State when an optimization is only a recommendation and has not been tested under load.
