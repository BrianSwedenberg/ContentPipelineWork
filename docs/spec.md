# SPEC.md — CONTENTPIPELINEWORK

## What this is
This is a project mainly targeted toward learning by doing.  Goal is to learn more about ai content generation through the completion of this project.

An AI-powered content generation pipeline for Brian's Dumpsters —
a commercial dumpster and portable toilet brokerage serving the
Charlotte NC metro area. This pipeline generates SEO-optimized
website content using a multi-agent loop built on the Anthropic API.

---

## The business
Brian's Dumpsters is a BROKER. It connects customers with vetted
local providers. It does not own or operate equipment.
All generated content must reflect this accurately.

Target markets: contractors, restaurant owners, property managers,
event organizers, and homeowners in the Charlotte NC metro area
and surrounding counties across NC and SC.

---

## What the pipeline produces
- City location pages (one per target city)
- Service pages (roll-off dumpster, commercial bin, porta potty)
- Blog and resource articles

---

## Agents and skills

| Skill file | Role |
|---|---|
| skills/brief-writer.md | Researches and structures content briefs |
| skills/writer-v2.md | Writes page content to the brief spec |
| skills/qa-editor.md | Scores and validates content, approves or rejects |
| skills/brand-voice.md | Brand voice reference — injected with Writer calls |

---

## Pipeline flow

```
brief (JSON) → Writer → QA Editor → approved? 
     ↑_____________ no (revision notes) ___|
                         ↓ yes
                    save to outputs/
```

- Max 3 revision attempts before escalating to human review
- QA approval threshold: score >= 85 AND all hard-fail checks pass
- All output saved as markdown to outputs/
- Full run log saved as JSON to outputs/run-logs/

---

## Key inputs

| File | Contents |
|---|---|
| inputs/briefs/ | One JSON brief per page |
| inputs/cities.csv | 42 cities across Charlotte metro |
| inputs/services.json | 3 service definitions |
| inputs/brief-schema.json | Master schema all briefs must follow |

---

## Hard rules
- Never fabricate permit info, landfill names, or local facts
- Never imply Brian's Dumpsters owns trucks or equipment
- Never publish content with is-active: true — always draft first
- Never commit .env or API keys to the repo

---

## Current phase
**Phase 1** — Single item pipeline. Writer + QA loop only.
Testing on Huntersville NC brief before scaling.

## Future phases
- Phase 2 — Add Tone Editor skill after Phase 1 is stable
- Phase 3 — Batch runner across full cities.csv
- Phase 4 — Push approved content to Google Drive
- Phase 5 — Push approved content to Webflow CMS