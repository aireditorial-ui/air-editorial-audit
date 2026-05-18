# AIR Editorial Audit Tool

A multi-pass editorial audit system built to catch what grammar checkers miss — argument structure failures, logic errors, and AI-generated word choices that flatten an author's voice. It runs a pipeline of specialized passes, each targeting a distinct failure category, rather than a single monolithic grammar check.

The AI Accent pass replaces AI-signature vocabulary with surgical, minimum-footprint edits that preserve the author's voice.

## Pass Pipeline

| Pass | What It Catches | Model |
|------|-----------------|-------|
| Structural Audit | Title/executive summary alignment; structural progression; whether novel data is positioned correctly | Claude Sonnet |
| Argument & Logic Audit | Conflation, non sequitur, unsupported causation, hidden dependency, equivocation, category error, intension/extension conflation | Claude Opus |
| Plain-English Summaries | Translates Phase 0 findings into plain language (no jargon) | Claude Sonnet |
| Charitable Interpretation Triage | Filters ambiguous findings before line-level passes run | Claude Sonnet |
| Integrity Pass | Cross-document factual and internal consistency | Claude Opus |
| Grammar & Style | Spelling, agreement, punctuation, CMOS number/date rules, comma splices, dangling modifiers, temporal inconsistencies | Claude Sonnet |
| Capitalization | Cargo-cult capitalization of abstract concepts (Digital Strategy, the Sector, Key Opinion Leaders) | Claude Sonnet |
| Prose | Functionless restatement, contradictory discourse markers | Claude Sonnet |
| AI Accent — Detection | Pattern-matches AI-signature vocabulary deterministically | Python only |
| AI Accent — Replacement | Generates voice-preserving replacements; guards against introducing words already present in surrounding context | Claude Haiku |
| Mechanical | Double spaces, punctuation errors, en-dash ranges, common confusables (rein/reign, pore/pour, affect/effect), UK→US spelling, gendered language | Python only |
| Named Entity Recognition | Intra-document consistency on proper nouns and named entities | Python + spaCy |

## Tech Stack

- Python / Flask
- Anthropic API (Claude Sonnet, Opus, Haiku)
- spaCy (en_core_web_trf) on Modal GPU (A10G)
- Microsoft Power Automate (workflow integration)
- python-docx / lxml (document processing)

## Roadmap

Next: Word add-in and Google Docs add-on — works inside the document natively via the Office JS and Google Workspace APIs, with tracked changes written directly to the file.

## Repo Note

This repository is documentation only. The codebase is private. No source code, prompts, or implementation details are included here.
