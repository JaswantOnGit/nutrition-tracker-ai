# UAT Checklist — AI-Powered Nutrition Tracking System

Testing went beyond the happy path before this was considered ready for daily use.

| # | Test Case | Input Example | Expected Behavior | Result |
|---|---|---|---|---|
| 1 | Standard meal, full detail | "Grilled chicken bowl for lunch, ~500 calories" | Parsed correctly, meal type inferred, entry written | ✅ Pass |
| 2 | Vague portion size | "Had some pasta" | Claude estimates conservatively and flags the estimate as approximate rather than stating it with false precision | ✅ Pass |
| 3 | No meal type specified | "Ate a protein bar" | Meal type defaults to a reasonable inference (snack) or is asked for — not left blank | ✅ Pass |
| 4 | Zero logs for the day | Progress check requested with no entries logged | Skill reports zero data clearly rather than defaulting to a misleading "on track" | ✅ Pass |
| 5 | Partial week of data | Progress check with 2 days logged | Skill does **not** claim a "consistent" pattern — states there isn't enough data yet | ✅ Pass |
| 6 | Multiple meals same day | Three separate meals logged across breakfast/lunch/dinner | Daily total formula correctly sums all three | ✅ Pass |
| 7 | Target changed mid-tracking | Macro Targets updated after several days of logs | Skill pulls the *current* target, doesn't use a stale cached value | ✅ Pass |
| 8 | Ambiguous / unusual food | "Had a weird leftover casserole thing" | Claude gives a best-effort estimate and explicitly flags low confidence | ✅ Pass |

**Sign-off:** All 8 cases passed before the system was used for daily tracking. Cases 5 and 4 were the ones most likely to produce a confidently wrong answer, and were prioritized accordingly.
