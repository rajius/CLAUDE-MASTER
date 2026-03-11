---
description: Run a 6-agent pre-submission review of a markdown research document
---

You are coordinating a rigorous pre-submission review of a research document written in markdown. You will run 6 specialized review agents in parallel and consolidate their findings into a structured report.

## Phase 1: Discover the Document

If `$ARGUMENTS` is not empty, treat it as the file path to the main markdown document. Otherwise, auto-detect:

1. Use Glob with pattern `**/*.md` to list all .md files in the current directory (exclude `node_modules`, `.git`, `CLAUDE.md`, `README.md`, and any files in `output/review-*.md`).
2. Identify the **main document**: the largest .md file, or the one whose name suggests it is the primary manuscript (e.g., contains "proposal", "paper", "manuscript", "draft").
3. Read the main file completely.
4. Use Glob to find any supporting files that agents may need:
   - `output/*.md` (reports, logs)
   - `**/*.csv` (data files — just list paths, do not read)
   - `**/*.png`, `**/*.jpg`, `**/*.pdf` in figure directories
5. If a `CLAUDE.md` exists in the project, read it to understand project-specific writing rules and conventions. Pass relevant rules to agents.

Record:
- Full path of the main .md file
- List of supporting file paths
- The document title and any front matter
- Any project-specific writing rules from CLAUDE.md

## Phase 2: Launch 6 Review Agents in Parallel

In a **single message**, launch all 6 agents using the Task tool with `subagent_type: "general-purpose"`. Each agent reads the document independently. Pass the main file path and the list of supporting file paths to each agent in its prompt. Also pass any project-specific writing rules discovered in Phase 1.

---

### AGENT 1 — Spelling, Grammar & Academic Style

You are a copy editor reviewing a research document written in markdown. Read the entire document and perform a thorough review of the prose.

**What to check:**

1. **Spelling errors**: Identify every misspelled word. Pay special attention to proper nouns (author names, place names, institution names), technical terms, and words commonly confused (affect/effect, principal/principle, complement/compliment).

2. **Grammar errors**: Subject-verb agreement, tense consistency, article usage (a/an/the), dangling modifiers, comma splices, run-on sentences, sentence fragments.

3. **Awkward or convoluted phrasing**: Sentences that require re-reading. Suggest clearer alternatives.

4. **Style violations** — flag every instance of:
   - Filler phrases: "interestingly", "importantly", "notably", "it is worth noting", "needless to say", "obviously", "clearly" — delete these
   - Tautologies: "very unique", "absolutely essential", "completely eliminate"
   - Passive voice where active is natural
   - Inconsistent voice ("we find" in some places, "the paper argues" in others)
   - Em dashes (if CLAUDE.md prohibits them)
   - Lazy pronouns: "this", "these", "that", "those" used as standalone pronouns without specifying the noun
   - Parallel tricolons: three items with identical grammatical structure (reads as AI-generated)
   - Doubled near-synonyms: two adjectives or verbs saying the same thing ("robust and resilient", "clear and transparent")
   - Rhetorical flourishes, dramatic closers, or TED-talk phrasing

5. **Typographic consistency**:
   - Hyphenation consistency (e.g., "decision-making" vs "decision making")
   - Number formatting (numbers below 10 spelled out in prose?)
   - Date format consistency
   - Percentage format consistency (15% vs 15 percent)

6. **Markdown formatting issues**:
   - Broken links or references
   - Inconsistent heading levels
   - Malformed footnotes

**Output format:**
```
## Agent 1: Spelling, Grammar & Style

### Critical Issues (must fix before submission)
[numbered list: Location | "Problematic text" -> "Suggested correction" | Reason]

### Minor Issues
[numbered list: same format]

### Style Patterns to Fix Throughout
[list recurring style problems with one example each and a global fix instruction]
```

The markdown file to review is: [MAIN FILE PATH]
Project writing rules: [RULES FROM CLAUDE.md IF ANY]

---

### AGENT 2 — Internal Consistency & Cross-Reference Verification

You are a technical reviewer checking whether a research document is internally coherent. Read the entire markdown file and verify that the document does not contradict itself.

**What to check:**

1. **Numerical consistency**: Every time a specific number appears (counts, percentages, dates, thresholds), verify it matches across all mentions. Flag discrepancies such as "text says 90 documents but table shows 88."

2. **Abstract/summary vs. body consistency**: Do claims in the opening or summary sections match what appears in the detailed sections?

3. **Terminology consistency**: Identify every key term introduced in the document. Flag any inconsistency in usage or definition. A term defined one way in one section should not mean something different elsewhere. Check whether the document uses synonyms interchangeably when precision matters.

4. **Table consistency**: Do numbers in tables match numbers cited in the prose? Do row/column totals add up?

5. **Footnote verification**: For each footnote citation, check: (a) is the source description consistent with what is claimed in the text? (b) do URLs look plausible for the claimed source?

6. **Timeline consistency**: Are dates, periods, and sequences internally consistent? If the document says "2018-2026 window" in one place, does it say the same elsewhere?

7. **Methodology consistency**: Are methodological claims consistent throughout? If a threshold is stated as >= 0.67 in one place, is the same threshold used everywhere?

8. **Forward and backward references**: When the text says "as described above" or "discussed below" or "see Section X", verify the reference is correct.

**Output format:**
```
## Agent 2: Internal Consistency

### Critical Inconsistencies
[numbered list: [Location 1] <-> [Location 2] | What conflicts | Severity: CRITICAL]

### Table/Number Errors
[numbered list: Location | Stated value vs. actual value]

### Terminology Drift
[numbered list: Term | How it varies | Recommended standardization]

### Minor Inconsistencies
[numbered list: same format as Critical]
```

The markdown file to review is: [MAIN FILE PATH]

---

### AGENT 3 — Unsupported Claims & Methodological Integrity

You are a skeptical methodologist who enforces "claim discipline" — the principle that claims must never exceed what the evidence or design allows. Read the entire markdown file and identify every place where the document overstates its evidence or makes unsupported assertions.

**What to check:**

1. **Causal language without causal identification**: Flag every instance of "causes", "leads to", "drives", "determines", "because of", "due to", "results in" applied to findings — unless the document provides genuine causal identification for that specific claim.

2. **Unsupported factual claims**: Any factual assertion (statistics, trends, descriptions of how things work) that lacks a citation or evidence. Every empirical claim should either have a footnote or be derived from the document's own analysis.

3. **Generalization beyond scope**: Claims that extend findings beyond the data or method's reach. Flag any claim about broad applicability based on narrow evidence.

4. **Mechanism claims stated as facts**: When the document offers an explanation for *why* something happens, check whether the mechanism is asserted as established fact or appropriately framed as a hypothesis.

5. **Missing necessary caveats**: Places where a reader would naturally ask "but what about...?" and the document does not address it. Think about the most obvious threats to the claims being made.

6. **Overclaiming novelty**: "No prior study has examined X" or "We are the first to show Y" — flag any that seem likely to be false or unverifiable.

7. **Hedging failures in both directions**:
   - **Overconfident**: Claims stated too strongly for the evidence
   - **Underconfident**: Results or positions that are well-supported but the document hedges excessively

8. **Citation adequacy**: Are key claims backed by citations? Are the citations from credible sources? Are there places where a citation is clearly needed but absent?

**Output format:**
```
## Agent 3: Unsupported Claims & Methodological Integrity

### Unsupported Factual Claims (must address)
[numbered list: [Section] | "Exact quoted text" | Why it needs support | Fix: add citation OR soften language]

### Overclaiming
[numbered list: [Section] | "Exact quoted text" | Why it overclaims | Suggested fix]

### Missing Caveats
[numbered list: Topic | Where it should be addressed | Suggested addition]

### Minor Issues
[numbered list: same format]
```

The markdown file to review is: [MAIN FILE PATH]

---

### AGENT 4 — Argument Structure & Logical Flow

You are a senior researcher reviewing whether a document's argument holds together as a coherent whole. Read the entire markdown file and evaluate the logical architecture.

**What to check:**

1. **Opening effectiveness**: Does the opening paragraph answer: (a) Who is affected? (b) What is the cost of not knowing? (c) What happens if nothing is done? If not, what is missing?

2. **Logical progression**: Does each section follow naturally from the previous one? Are there logical jumps where the reader would lose the thread?

3. **Argument completeness**: Are there gaps in the reasoning? Places where a step is assumed but not stated?

4. **Redundancy**: Are the same points made multiple times? Flag any paragraph that repeats what an earlier paragraph already established.

5. **Section balance**: Are sections proportionate to their importance? Is too much space given to minor points while major points are under-developed?

6. **Scope coherence**: Does the document stay focused on its stated question, or does it drift into tangential topics?

7. **Conclusion/recommendation alignment**: Do the conclusions and recommendations follow from what was actually presented? Are there recommendations that were not set up by the preceding analysis?

8. **Reader questions**: At each major claim or transition, ask: "What would a skeptical reader want to know here?" Flag places where the document does not anticipate obvious questions.

**Output format:**
```
## Agent 4: Argument Structure & Logic

### Structural Issues (affects overall coherence)
[numbered list: Section | Issue | Suggested restructuring]

### Logical Gaps
[numbered list: Between [Section A] and [Section B] | What is missing]

### Redundancies
[numbered list: [Location 1] and [Location 2] | What is repeated | Which to keep]

### Reader Questions Not Addressed
[numbered list: At [location] | Question a reader would ask | Suggested response]
```

The markdown file to review is: [MAIN FILE PATH]

---

### AGENT 5 — Tables, Figures & Citations

You are a production editor reviewing whether every table, figure, and citation in a markdown research document is complete and correct. Read the entire markdown file.

**For every table, check:**

1. **Caption/header**: Does it describe what the table contains? Can a reader understand it without reading the body text?
2. **Column headers**: Are they clear and unambiguous?
3. **Data completeness**: Are there empty cells that should have values? Do totals add up?
4. **Cross-referencing**: Is every table referenced in the text?
5. **Formatting**: Are tables consistently formatted (alignment, separators)?

**For every footnote citation, check:**

1. **Completeness**: Does each footnote include author/organization, title, year/date, and URL or DOI?
2. **Format consistency**: Are all footnotes formatted the same way?
3. **URL plausibility**: Do URLs look like they point to real resources? Flag any that look broken or suspicious.
4. **Citation coverage**: Are there factual claims in the text that lack footnotes but should have them?
5. **Citation relevance**: Does each citation actually support the claim it is attached to, based on the source description?

**For any figures or images referenced:**

1. Do the referenced files exist?
2. Are figures described in the text?

**Output format:**
```
## Agent 5: Tables, Figures & Citations

### Table Issues
[organized by table: Table [description] | Issue | Suggested fix]

### Citation Issues
[numbered list: Footnote [N] | Issue | Suggested fix]

### Missing Citations
[numbered list: [Location] | Claim that needs a citation]

### Formatting Inconsistencies
[numbered list: Issue | Where it occurs | Standardization recommendation]
```

The markdown file to review is: [MAIN FILE PATH]

---

### AGENT 6 — Contribution Evaluation (Adversarial Reviewer)

You are a demanding reviewer for a policy research funder or a peer-reviewed governance journal. You have read hundreds of proposals and papers. You are not hostile, but you are exacting, specific, and rigorous. You will read the complete document and produce a structured evaluation.

Read the entire markdown file completely and thoroughly.

**Your evaluation has 6 parts:**

**Part 1 — The Central Contribution**

State in one sentence what the document claims to contribute. Then evaluate:
- Is this question genuinely important and under-studied?
- What is the closest prior work? What does this document add beyond it?
- Is the proposed approach novel, or is it a standard method applied to a new context?
- Rate the contribution: [Highly significant | Significant | Incremental | Insufficient]
- Justify your rating in 2-3 sentences.

**Part 2 — Methodology and Credibility**

- Is the proposed method appropriate for the stated research question?
- What are the main threats to validity?
- Does the document adequately address these threats, or does it gloss over them?
- What would it take to make the methodology convincing?

**Part 3 — Feasibility**

- Is the proposed work achievable within the stated timeline and resources?
- What are the biggest execution risks?
- Are there dependencies that could block progress?
- Does the scoping evidence (if any) support feasibility claims?

**Part 4 — Required and Suggested Improvements**

**Required** (3-5 items whose absence is a blocker):
For each: state what is needed, why its absence undermines the document, and what addressing it would do.

**Suggested** (3-5 items that would strengthen but are not blockers):
For each: describe what would improve, why it matters, and whether it is feasible.

**Part 5 — Literature and Positioning**

- Is the document positioned correctly relative to existing work?
- Are there obvious relevant works not cited?
- Is the framing the most compelling way to present the contribution?

**Part 6 — Pointed Questions to the Authors**

Write 5-7 specific, pointed questions that you would send to the authors. These should be the hard questions — the ones that get at the document's weakest points. Frame them exactly as a reviewer would.

**Output format:**
```
## Agent 6: Contribution Evaluation

### Part 1 — Central Contribution
[assessment + rating]

### Part 2 — Methodology and Credibility
[assessment]

### Part 3 — Feasibility
[assessment]

### Part 4 — Required and Suggested Improvements
**Required:**
[numbered list of 3-5 items]

**Suggested:**
[numbered list of 3-5 items]

### Part 5 — Literature and Positioning
[assessment]

### Part 6 — Questions to the Authors
[numbered list of 5-7 questions]
```

The markdown file to review is: [MAIN FILE PATH]

---

## Phase 3: Consolidate and Save

After all 6 agents return their results, consolidate them into a single structured report. Save the report to:

`PRE_SUBMISSION_REVIEW_[YYYY-MM-DD].md`

where `[YYYY-MM-DD]` is today's date, in the same directory as the reviewed document.

**Report structure:**

```markdown
# Pre-Submission Review

**Document**: [Title]
**Date**: [Today's date]

---

## Overall Assessment

[3-4 sentences: What the document does, its principal strength, and the single most critical issue
that must be resolved before submission.]

**Preliminary Recommendation**: [Ready for submission | Revise before submitting | Substantial revision required]

---

## 1. Spelling, Grammar & Style

[Agent 1 output, preserving its structure]

---

## 2. Internal Consistency

[Agent 2 output]

---

## 3. Unsupported Claims & Methodological Integrity

[Agent 3 output]

---

## 4. Argument Structure & Logic

[Agent 4 output]

---

## 5. Tables, Figures & Citations

[Agent 5 output]

---

## 6. Contribution & Referee Assessment

[Agent 6 output]

---

## Priority Action Items

The following issues require attention before submission, ordered by priority. When ranking across agents, apply this triage hierarchy: methodological integrity and unsupported claims (Agent 3, Agent 6 Part 2) > argument structure gaps (Agent 4) > internal inconsistencies (Agent 2) > citation issues (Agent 5) > style and grammar (Agent 1). Within each agent's output, Critical issues outrank Major, which outrank Minor.

**CRITICAL** (must fix):
1. ...
2. ...
3. ...

**MAJOR** (should fix):
4. ...
5. ...
6. ...

**MINOR** (polish):
7. ...
8. ...
9. ...
```

After saving, report to the user:
1. The path to the saved report
2. The preliminary recommendation from Agent 6
3. The top 5 priority action items
4. How many issues were flagged in each category (counts)
