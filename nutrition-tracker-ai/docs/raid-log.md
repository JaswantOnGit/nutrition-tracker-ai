# RAID Log — AI-Powered Nutrition Tracking System

## Risks

| ID | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| R1 | Claude misestimates macros on an ambiguous meal description ("a bowl of pasta") | High | Medium | Confirm-before-write pattern — parsed entry is shown to the user before it commits to Notion |
| R2 | Skill overstates a "pattern" from insufficient data (e.g., 1 day logged) | Medium | Low | Skill logic explicitly requires 3+ tracked days before calling anything "consistent" |
| R3 | Connector auth token expires or is revoked, silently breaking writes | Low | Medium | Periodic manual verification; write confirmation surfaced to user every time, so a silent failure would be visible immediately |
| R4 | Formula fields in Notion break if a property is renamed or deleted | Low | Medium | Schema documented in this repo; changes should be tested against the formula dependencies before deploying |

## Assumptions

| ID | Assumption | Validation |
|---|---|---|
| A1 | User will review and confirm each parsed entry before it writes to Notion | Built into the interaction flow — not a passive assumption, an enforced step |
| A2 | Free-tier Claude.ai usage limits are sufficient for daily single-user logging | Held true across testing; would need re-validation at higher usage volume |
| A3 | Text-only meal descriptions provide enough signal for reasonable macro estimates | Acceptable for common foods; flagged as a real limitation for ambiguous or unusual meals |

## Issues

| ID | Issue | Status | Resolution |
|---|---|---|---|
| I1 | Initial Skill version used fixed, hardcoded macro targets | Resolved | Refactored to pull targets dynamically from the `Macro Targets` database each time, so it stays accurate if goals change |
| I2 | Early pattern-detection logic in the Skill would call a macro "consistently" over/under target even with only one day of data | Resolved | Added a minimum-data threshold (3+ tracked days) before any consistency claim is made |

## Dependencies

| ID | Dependency | Owner | Notes |
|---|---|---|---|
| D1 | Notion connector authentication (Claude.ai side) | Anthropic / Notion | Required before any read/write is possible |
| D2 | Notion database schema (`Calorie Logs`, `Macro Targets`) | Self | Must exist and be correctly related before the Skill can query it |
| D3 | Claude Project persistent instructions | Self | Skill and logging behavior depend on these being current and accurate |
