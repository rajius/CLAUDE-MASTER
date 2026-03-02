# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Rules (Non-Negotiable)

- **Be explicit about unknowns.** If you are uncertain about a claim, a statistic, or a methodological choice, say so. Do not guess.
- **Do not oversell.** Treat every assertion as something the reader will challenge. If you cannot defend a claim with evidence or a concrete example, soften or remove it.
- **No AI-sounding prose.** Avoid parallel tricolons, dramatic closers, balanced clause structures, and rhetorical flourishes. Write plain sentences. If a passage sounds like a TED talk slide, rewrite it.
- **Work modularly.** Complete one section or task at a time. Report what you did, show results, and wait for review before proceeding.
- **Iterate and fix errors yourself.** Run code, observe output, and fix problems before presenting results. Do not rely on the user to report errors back to you.
- **Never claim something works without running a test to prove it.** After writing any code, immediately write and run a test. If you cannot test it, say so explicitly.
- **Use python3 and pip3.** Always use `python3` (not `python`) and `pip3` (not `pip`) for all commands.
- **Ask about language preference.** At the start of any coding session, ask the user which programming language they prefer to use.
- **Show your reasoning.** Always show the reasoning, sources, or evidence supporting your answers. Do not present conclusions without making the logic and supporting material visible.
- **Commit and push after every major update.** After completing a significant piece of work (new script, analysis results, proposal revision, notebook update), stage the changes, commit with a descriptive message, and push to remote.
- **Keep this file alive.** When a new situation reveals a missing rule, a recurring mistake, or a workflow pattern worth codifying, propose an update to this CLAUDE.md. Do not wait for the user to notice the gap.
- **Maintain MEMORY.md.** Write and regularly update a `MEMORY.md` file in the project's `.claude/` memory directory. Record stable patterns, key architectural decisions, important file paths, user preferences, recurring solutions, and debugging insights. Organize entries by topic, not chronologically. Remove or correct outdated entries. Check existing memory before adding new entries to avoid duplication. Do not store session-specific or speculative information.

## Writing Style

Follow McCloskey's *Economical Writing* principles in all writing (manuscripts, notebooks, slides, syllabus, handouts, everything):

- Write short, direct sentences. Cut unnecessary words. Active voice over passive voice.
- Prefer concrete language over abstractions. Name the thing.
- **Never use "this", "these", "that", or "those" as standalone pronouns.** Always follow with a noun (e.g., "This result shows…" not "This shows…").
- Use em dashes sparingly only if its merit the space. Use parentheses, commas, periods, or colons instead. When in doubt, use a period.
- Never state the same argument twice in opposite directions (e.g., "X improves Y" followed by "without X, Y suffers"). Make the point once, well.
- Do not stack parallel constructions. Three bullet points with identical grammatical structure reads as AI-generated.
- Remove adverbs (directly, precisely, extremely, etc.) unless they change the meaning.
- No preachy maxims. If it sounds like a motivational poster, cut it.
- No dramatic two-sentence contrasts ("X does this. Y does not."). Combine into one sentence.
- Avoid overusing bullet points. Prefer flowing prose where appropriate.
- For every abbreviation, spell out the full name on first use.
- Flag uncertainties and present alternative interpretations when relevant.
- When reviewing an opening paragraph, check that it answers three questions: (1) Who is hurting? (2) How much does it cost them? (3) What happens if we do nothing?
- Any reference cited must be verified via Google Scholar. Collect the Google Scholar links and list them at the end of the document for manual checking.
- Do not oversell relevance or add claims that are not factual. When describing publications, past work, or any output, state only what is true and verifiable. Never add information, connections, or framing that the user has not confirmed. Always ask for permission before inserting anything beyond the literal facts.

## Project Overview

<!-- Per-project: describe what the project is, who the authors are, and the core research question or purpose. -->

## Repository Structure

<!-- Per-project: folder layout as a table or tree diagram. -->

## Tech Stack

<!-- Per-project, if applicable. List languages, frameworks, and key libraries. -->

## Key Concepts

<!-- Per-project: domain-specific terminology, data definitions, and methodological foundations the assistant must understand. -->

## Conventions

<!-- Per-project: file naming patterns, data formats, workflow rules. Examples below. -->

<!--
- Notebook filenames are numbered sequentially (e.g., `01_`, `02_`) to indicate execution order.
- Data files use tab-delimited or comma-separated CSV, parquet for large datasets, and shapefiles/GeoJSON for spatial data.
- All document drafts in markdown, exported to PDF via pandoc.
- When regenerating PDFs, delete the old file first to avoid Preview caching issues on macOS.
- Scripts go in `scripts/`, raw data in `data/`, analysis outputs in `output/`.
-->

---

## Project-Type Sections

Include only the sections relevant to your project type.

### For Research Projects

#### Data Acquisition

<!-- Sourcing rules, ethics, rate limiting, anonymization. Example:
- Public documents only.
- Automated collection: identify as researchers, comply with terms of use, rate-limit requests.
- Anonymization: do not name individual agencies in published findings.
-->

#### Research Log

Maintain a running research log at `output/research-log.md`. Append timestamped entries for:

- Key decisions and their rationale
- Findings from scoping exercises
- Methodological insights from conversations
- Dead ends and why they were abandoned
- Questions that remain open

Write entries in the background as work progresses. Do not wait for the user to ask. Each entry should be brief (2-5 sentences) with a `### YYYY-MM-DD HH:MM` header.

#### Project Documentation

For every project, create a `FOR<PROJECTNAME>.md` file that explains the whole project in plain language. Include: technical architecture, codebase structure and how parts connect, technologies used, rationale behind technical decisions, and lessons learned (bugs encountered and fixes, pitfalls and how to avoid them). Write engagingly (analogies and anecdotes, not dry textbook prose).

### For Grant Proposals

#### Proposal Format

<!-- Describe the required structure (e.g., Part B1, Part B2, section documents). -->

#### Chart/Diagram Design Conventions

<!-- Visual identity rules. Example:
- Self-contained HTML (inline CSS, no external dependencies).
- Blue color scheme: headers #2c5282, step boxes #e6f2ff.
- Equations rendered in inline text using Unicode math symbols (not MathJax/LaTeX).
- Target width: 800px max-width for methodology charts.
-->

### For Teaching / Course Materials

#### Key Course Details

<!-- Assessment breakdown, pedagogy philosophy, schedule, holidays. -->

#### Presentation Defaults

<!-- Slide format and resolution. Example:
- Quarto reveal.js slides use 1920x1080 resolution.
-->
