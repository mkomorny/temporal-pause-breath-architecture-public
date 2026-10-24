# Temporal, Pause & Breath Architecture

> **Tri-Platform Agent Skill** for Claude Desktop / Code, Grok CLI, and Google Antigravity / Gemini.  
> Conversational Pause and Respiration Timing — Generates exhaustive Temporal, Pause & Breath Architecture reports detailing speech timing, pause duration histograms, pause-to-speech ratio, inhalation acoustics, intra-phrase velocity, and nPVI rhythm.

---

## Overview

`temporal-pause-breath-architecture` provides standardized capabilities across conversational AI platforms:
- Pause duration histogram and statistical modeling (micropauses vs macro/clause pauses).
- Inhalation duration, audibility, and glottal sound pressure modeling.
- Normalized Pairwise Variability Index (nPVI) vocal rhythm calculation.
- Filled-pause vowel acoustics ('uh', 'um') and pitch contours.
- Standardized temporal_pause_architecture.json schema.
- Tri-platform NTFS junctions connecting Claude, Grok, and Antigravity.
- Standard documentation suite: SKILL.md, HOW_TO_USE.txt, IMPLEMENTATION_PLAN.md, and README.md.

---

## Tri-Platform Architecture

Zero duplicate code across platforms. Canonical source resides in `.agents`:
- **Canonical Source**: `C:\Users\<you>\.agents\skills\temporal-pause-breath-architecture`
- **Claude**: `C:\Users\<you>\.claude\skills\temporal-pause-breath-architecture` (NTFS Junction)
- **Grok**: `C:\Users\<you>\.grok\skills\temporal-pause-breath-architecture` (NTFS Junction)
- **Antigravity**: `C:\Users\<you>\.gemini\config\skills\temporal-pause-breath-architecture` (NTFS Junction)

---

## Documentation Suite

- [`HOW_TO_USE.txt`](HOW_TO_USE.txt): Standardized user guide and prompt templates.
- [`IMPLEMENTATION_PLAN.md`](IMPLEMENTATION_PLAN.md): Feature checklist and roadmap.
- [`App Changes Tracker.html`](App%20Changes%20Tracker.html): Interactive visual version log.
- [`SKILL.md`](SKILL.md): Agent system instructions and triggers.
