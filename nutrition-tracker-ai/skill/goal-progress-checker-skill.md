# Skill Spec — Goal Progress Checker

## Purpose

A Claude Skill that, when activated, analyzes logged nutrition data against daily targets and returns a concise, honest progress summary — without requiring the user to manually pull and calculate totals from Notion.

## Trigger Conditions

Activated when the user asks a variant of:
- "How am I doing?"
- "Progress check"
- "Am I on track today / this week?"

## Logic

1. **Pull targets dynamically** from the `Macro Targets` database (Target Calories, Protein Target, Carbs Target, Fats Target) rather than assuming fixed values — so it stays accurate if goals change.
2. **Retrieve logs** for the requested period (defaults to current week, or a user-specified range) from `Calorie Logs`.
3. **Group by day** and compare actual daily averages against targets.
4. **Flag gaps conservatively** — a macro is only called "consistently under" or "consistently over" if it's off-target on more than half of *tracked* days, and only if at least 3 days of data exist. With fewer than 3 days, the Skill states plainly that there isn't enough data for a pattern claim yet.
5. **Surface one specific, evidence-based insight** rather than a generic summary — e.g., a shortfall macro paired with a food suggestion that's mindful of macros already close to target, not a repeated boilerplate tip.

## Output Format

- Days tracked (of the requested period)
- Average daily calories vs. target
- Average macros vs. targets, with over/under/on-track status per macro
- One specific, data-backed insight or suggestion

## Failure Handling

- **No logs for the period:** state this plainly — never default to "on track" with zero data.
- **Insufficient data for a pattern claim:** explicitly say so rather than inferring a trend from 1–2 days.
- **Missing target data:** flag that targets haven't been set rather than comparing against an assumed default.

## Design Rationale

This was built as a Skill rather than a one-off prompt so the logic is reusable across sessions without re-explaining it — and so it can be improved once (e.g., adding the minimum-data threshold) instead of being re-fixed in every conversation. See [`../docs/raid-log.md`](../docs/raid-log.md) issues I1–I2 for how this logic was iterated on after initial testing.
