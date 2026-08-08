# RACI Matrix — AI-Powered Nutrition Tracking System

Solo project — but ownership is still mapped explicitly by **function**, not by person. On a team implementation, each row below is where a distinct role would sit.

| Activity | Responsible | Accountable | Consulted | Informed |
|---|---|---|---|---|
| Define daily calorie/macro targets | User | User | — | Claude Project (reads targets) |
| Parse meal description into structured data | Claude (reasoning layer) | Implementer | — | User |
| Validate parsed entry before write | User | User | Claude (flags ambiguity) | — |
| Write entry to Notion | Notion Connector | Implementer | — | User |
| Maintain database schema (relations, formulas) | Implementer | Implementer | — | — |
| Define Skill trigger logic and thresholds | Implementer | Implementer | — | User |
| Run and interpret progress check | Claude Skill | User | — | — |
| Own data accuracy over time | User | User | Claude (surfaces discrepancies) | — |

**Why this matters even solo:** on any real implementation, "who confirms the AI's output is correct" and "who owns the underlying data" are different people. Mapping that explicitly here — rather than assuming one person does everything — is the habit that carries over to a multi-stakeholder engagement.
