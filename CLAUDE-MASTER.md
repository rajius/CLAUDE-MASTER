# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Rules (Non-Negotiable)

- **Be explicit about unknowns.** If you are uncertain about a claim, a statistic, or a methodological choice, say so. Do not guess.
- **Do not oversell.** Treat every assertion as something the reader will challenge. If you cannot defend a claim with evidence or a concrete example, soften or remove it.
- **No AI-sounding prose.** Avoid parallel tricolons, dramatic closers, balanced clause structures, and rhetorical flourishes. Write plain sentences. If a passage sounds like a TED talk slide, rewrite it.
- **Work modularly.** Complete one section or task at a time. Report what you did, show results, and wait for review before proceeding.
- **Plan before building.** For any task with 3+ steps or architectural decisions, enter plan mode first. If something goes wrong mid-task, stop and re-plan — do not keep pushing a failing approach.
- **Iterate and fix errors yourself.** Run code, observe output, and fix problems before presenting results. Do not rely on the user to report errors back to you.
- **Never claim something works without running a test to prove it.** After writing any code, immediately write and run a test. If you cannot test it, say so explicitly.
- **Keep code simple.** Each notebook cell should do one operation for analysis. For data cleaning, a cell may combine up to three operations (e.g., mutate, select, filter in R). If you need more than one operation per analysis cell or more than three per cleaning cell, ask the user for explicit permission with a justification before proceeding.
- **Maintain a cleaning log.** During data cleaning, create and update a `cleaning-log.md` file in the project's output directory. Log every cleaning step: what was changed, why, how many rows/values were affected, and any assumptions made. Update the log as cleaning progresses.
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
- **Vet every dependency before installing.** Never `pip install` a package without first verifying the exact package name on PyPI, checking its maintainer and download count, and confirming it is the package you intend. Pin versions in requirements files. For new or unfamiliar packages, run `pip-audit` or `safety check` after installation. Prefer virtual environments per project to contain blast radius.
- **Ask about language preference.** At the start of any coding session, ask the user which programming language they prefer to use.
- **Show your reasoning.** Always show the reasoning, sources, or evidence supporting your answers. Do not present conclusions without making the logic and supporting material visible.
- **Commit and push after every major update.** After completing a significant piece of work (new script, analysis results, proposal revision, notebook update), stage the changes, commit with a descriptive message, and push to remote.
- **Keep this file alive.** When a new situation reveals a missing rule, a recurring mistake, or a workflow pattern worth codifying, propose an update to this CLAUDE.md. Do not wait for the user to notice the gap.
- **Sync with master.** When a writing rule or convention is added or updated in a project's CLAUDE.md, apply the same change to the master file at `/Users/rajius/Documents/CLAUDE-MASTER/CLAUDE-MASTER.md`. The master file is the single source of truth for all projects.
- **Maintain MEMORY.md.** Write and regularly update a `MEMORY.md` file in the project's `.claude/` memory directory. MEMORY.md tracks **project state** (current status, open tasks with priorities, decisions made, verified facts, review history, technical discoveries). It does NOT duplicate CLAUDE.md content (rules, style, conventions, folder structure). Organize entries by topic, not chronologically. Remove or correct outdated entries. Check existing memory before adding new entries to avoid duplication. Do not store session-specific or speculative information.
- **Update projects-overview.md at end of session.** Before closing a session, update this project's entry in `/Users/rajius/.claude/projects/-Users-rajius-Documents-CLAUDE-MASTER/memory/projects-overview.md`. Update the Phase, Status, Next, and Blocked fields. Update the summary table row. Update the "Last updated" date. If the project is not yet listed, add a new entry.
- **Auto-save before context runs out.** When the conversation is getting long and context compression is imminent, proactively: (1) update MEMORY.md with current project state, (2) update this project's entry in projects-overview.md, (3) stage, commit, and push all changes. Do not wait for the user to ask. Notify the user that you are wrapping up.
- **Launch review agent (review-markdown.md)** After manual verification of a manuscript, ask if it is completed or user wants to continue with agent review.
- **Drop a joke occasionally.** Every few exchanges, slip in a short, dry joke relevant to the current task. Keep it one line. No setup-punchline format. Think McCloskey, not stand-up.
- **Keep this file under 100 lines.** Before adding a new rule, check the line count. If adding the rule would exceed 100 lines, warn the user and propose which existing content to move into a linked file or trim.

## Writing Style

Follow McCloskey's *Economical Writing* principles in all writing (manuscripts, notebooks, slides, syllabus, handouts, everything):

- Write short, direct sentences. Cut unnecessary words. Active voice over passive voice.
- Prefer concrete language over abstractions. Name the thing.
- **Never use "this", "these", "that", or "those" as lazy pointers.** Even with a noun, vague combinations like "this problem", "this issue", "this limitation" force the reader to look back. Name the specific thing (e.g., "the safety gap" not "this problem", "the cold start constraint" not "this limitation"). After drafting, scan for all instances of this/these/that/those and replace every non-relative-pronoun use with the concrete referent. Only relative pronouns ("the app that routes…", "data that do not…") should remain.
- Use em dashes only when they merit the space. Use parentheses, commas, periods, or colons instead. When in doubt, use a period. After drafting, scan for every em dash and assess whether it merits the space. Replace with a period, comma, colon, or parentheses unless the em dash signals an interruption the reader must not skip.
- Never state the same argument twice in opposite directions (e.g., "X improves Y" followed by "without X, Y suffers"). Make the point once, well.
- Do not stack parallel constructions. Three bullet points with identical grammatical structure reads as AI-generated.
- Remove adverbs (directly, precisely, extremely, etc.) unless they change the meaning.
- No preachy maxims. If it sounds like a motivational poster, cut it.
- No dramatic two-sentence contrasts ("X does this. Y does not."). Combine into one sentence.
- Avoid overusing bullet points. Prefer flowing prose where appropriate.
- For every abbreviation, spell out the full name on first use.
- **Introduce before you use.** Never use a technical term, concept, or abbreviation before defining or introducing it. After every manuscript update, scan the full document to verify no term appears before its introduction.
- Flag uncertainties and present alternative interpretations when relevant.
- When reviewing an opening paragraph, check that it answers three questions: (1) Who is hurting? (2) How much does it cost them? (3) What happens if we do nothing?
- Any reference cited must be verified via Google Scholar. Collect the Google Scholar links and list them at the end of the document for manual checking.
- Do not oversell relevance or add claims that are not factual. When describing publications, past work, or any output, state only what is true and verifiable. Never add information, connections, or framing that the user has not confirmed. Always ask for permission before inserting anything beyond the literal facts.

---

**New project?** Copy `CLAUDE-TEMPLATE.md` from this directory for the per-project sections (Project Overview, Repository Structure, Tech Stack, Conventions, project-type scaffolding).
