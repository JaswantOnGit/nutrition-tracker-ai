# Project Charter — AI-Powered Nutrition Tracking System

## Purpose

Build a conversational meal-logging system that lets a user log food intake through natural language, with Claude handling parsing and macro estimation and Notion serving as the persistent, structured data store.

## Business Case

Manual nutrition tracking has a high drop-off rate — the friction of opening an app and filling in fields daily is usually what kills adherence, not lack of motivation. Removing that friction (plain conversation instead of a form) was the core hypothesis being tested.

## Scope

**In scope**
- Natural-language meal logging → structured Notion write
- Two related Notion databases: `Calorie Logs`, `Macro Targets`
- Live formula-driven daily totals and % macro breakdowns
- A persistent Claude Project with standing instructions (goals, tracker structure, logging rules)
- A packaged Claude Skill (`Goal Progress Checker`) for on-demand progress review

**Out of scope**
- Image-based food logging (photo → macro estimation)
- Multi-user support / shared workspace access
- Automated reminders or scheduled check-ins
- Integration with wearables or fitness trackers

Scope was deliberately kept tight — the goal was to validate the interaction pattern (conversational input → governed data store → on-demand analysis), not to build a full nutrition app.

## Stakeholders

| Role | Owner |
|---|---|
| Sponsor / end user | Jaswant Singh |
| Implementation | Jaswant Singh |
| Data accuracy reviewer | Jaswant Singh (user confirms every entry before write) |

*(Solo project — RACI still mapped explicitly. See [`raci-matrix.md`](raci-matrix.md).)*

## Success Criteria

1. A meal described in plain language is correctly parsed into calories, protein, carbs, and fats.
2. The structured entry writes to Notion without manual intervention.
3. Daily totals and % breakdowns update live via formula, not manual recalculation.
4. The Goal Progress Checker Skill correctly compares actual vs. target and does not overstate confidence on limited data (e.g., does not claim a "consistent pattern" from a single day of logs).

## Constraints

- Free-tier Claude.ai and Notion accounts
- No custom backend — all logic lives in Claude Project instructions and a Claude Skill
- Estimation accuracy is bounded by what can be inferred from a text description alone (no photo/label input)

## Timeline

Single-session build: connector setup → template exploration → personalization → Project setup → Skill build and refinement. Approx. 1–2 hours end to end.
