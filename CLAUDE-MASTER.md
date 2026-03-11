# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Rules (Non-Negotiable)

- **Be explicit about unknowns.** If you are uncertain about a claim, a statistic, or a methodological choice, say so. Do not guess.
- **Do not oversell.** Treat every assertion as something the reader will challenge. If you cannot defend a claim with evidence or a concrete example, soften or remove it.
- **No AI-sounding prose.** Avoid parallel tricolons, dramatic closers, balanced clause structures, and rhetorical flourishes. Write plain sentences. If a passage sounds like a TED talk slide, rewrite it.
- **Work modularly.** Complete one section or task at a time. Report what you did, show results, and wait for review before proceeding.
- **Iterate and fix errors yourself.** Run code, observe output, and fix problems before presenting results. Do not rely on the user to report errors back to you.
- **Never claim something works without running a test to prove it.** After writing any code, immediately write and run a test. If you cannot test it, say so explicitly.
- **Keep code simple.** Each notebook cell should do one operation for analysis. For data cleaning, a cell may combine up to three operations (e.g., mutate, select, filter in R). If you need more than one operation per analysis cell or more than three per cleaning cell, ask the user for explicit permission with a justification before proceeding.
- **Comment every notebook cell.** Every code cell must have a markdown cell before and after it.
  - **Before cell:** State the goal, the input, the output, and the operations. Format: "Create `[output]` from `[input]` by [operation(s)]."
  - **After cell:** Discuss findings, flag anomalies, note interpretation, or record next steps. If the output is self-explanatory, a one-line confirmation is enough.
  - **Example:**

    > **Markdown cell (before):**
    > Create `df` from `raw_df` by filtering rows where year >= 2020 and selecting columns city, population, and pkb_share.
    >
    > **Code cell:**
    > `df <- raw_df %>% filter(year >= 2020) %>% select(city, population, pkb_share)`
    >
    > **Markdown cell (after):**
    > df has 342 rows across 15 cities, as expected. No missing values in pkb_share.
- **Use python3 and pip3.** Always use `python3` (not `python`) and `pip3` (not `pip`) for all commands.
- **Ask about language preference.** At the start of any coding session, ask the user which programming language they prefer to use.
- **Show your reasoning.** Always show the reasoning, sources, or evidence supporting your answers. Do not present conclusions without making the logic and supporting material visible.
- **Commit and push after every major update.** After completing a significant piece of work (new script, analysis results, proposal revision, notebook update), stage the changes, commit with a descriptive message, and push to remote.
- **Keep this file alive.** When a new situation reveals a missing rule, a recurring mistake, or a workflow pattern worth codifying, propose an update to this CLAUDE.md. Do not wait for the user to notice the gap.
- **Sync with master.** When a writing rule or convention is added or updated in a project's CLAUDE.md, apply the same change to the master file at `/Users/rajius/Documents/CLAUDE-MASTER/CLAUDE-MASTER.md`. The master file is the single source of truth for all projects.
- **Maintain MEMORY.md.** Write and regularly update a `MEMORY.md` file in the project's `.claude/` memory directory. MEMORY.md tracks **project state** (current status, open tasks with priorities, decisions made, verified facts, review history, technical discoveries). It does NOT duplicate CLAUDE.md content (rules, style, conventions, folder structure). Organize entries by topic, not chronologically. Remove or correct outdated entries. Check existing memory before adding new entries to avoid duplication. Do not store session-specific or speculative information.
- **Update projects-overview.md at end of session.** Before closing a session, update this project's entry in `/Users/rajius/.claude/projects/-Users-rajius-Documents-CLAUDE-MASTER/memory/projects-overview.md`. Update the Phase, Status, Next, and Blocked fields. Update the summary table row. Update the "Last updated" date. If the project is not yet listed, add a new entry.
- **Auto-save before context runs out.** When the conversation is getting long and context compression is imminent, proactively: (1) update MEMORY.md with current project state, (2) update this project's entry in projects-overview.md, (3) stage, commit, and push all changes. Do not wait for the user to ask. Notify the user that you are wrapping up.
- **Launch review agent (review-markdown.md)** After manual verification of a manuscript, ask if it is completed or user wants to continue with agent review.

## Writing Style

Follow McCloskey's *Economical Writing* principles in all writing (manuscripts, notebooks, slides, syllabus, handouts, everything):

- Write short, direct sentences. Cut unnecessary words. Active voice over passive voice.
- Prefer concrete language over abstractions. Name the thing.
- **Never use "this", "these", "that", or "those" as lazy pointers.** Even with a noun, vague combinations like "this problem", "this issue", "this limitation" force the reader to look back. Name the specific thing (e.g., "the safety gap" not "this problem", "the cold start constraint" not "this limitation"). After drafting, scan for all instances of this/these/that/those and replace every non-relative-pronoun use with the concrete referent. Only relative pronouns ("the app that routes…", "data that do not…") should remain.
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
