# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this project is

**Pod 4 — Capability & Talent Strength.** This is not a software codebase. It is
a working space for designing and consolidating a **staff survey questionnaire**
on talent development and career pathing at Gentari.

The deliverables are documents and data (survey questions, a consolidated
spreadsheet), not application code.

## Background & problem statement

Across the Gentari group there are **no, or inadequate, structured rules /
frameworks** for talent development and career-path programs. This gap can
hinder the growth and promotion of talent in both:

- **Technical groups** — engineering and project management
- **Non-technical groups** — all other functions

## Main objective

**Talent growth and retention are constrained (issue)** due to **insufficient
structured development and unclear capability pathways (root cause)**, leading
to a **weakened talent pipeline and reduced organisational capability (impact)**
to deliver the **$613 million EBITDA target for 2030**.

Validate this problem by running a **quick survey** to Gentari staff across
markets, deliberately covering both technical and non-technical staff. The survey
findings should evidence whether the talent-development / career-path gap is real
and where it bites hardest.

## How the questions are gathered

- Each Pod contributor proposes **3 potential questions** for the questionnaire.
- Questions are collected from contributors, then **consolidated into a single
  Excel file** as the master list for the questionnaire sent to targeted staff.

## Latest questionnaire

`deliverables/Survey_Question_Master_List.md` is the **single source of truth**
for the survey questions — the only questions file Claude should ever refer to
when asked about the questionnaire (question count, content, themes, etc.).
Do not answer questions-related queries from any other file, memory, or guess.

- `deliverables/Survey_Question_Master_List.md` — **always read this one** for
  the up-to-date set of questions. It's a Markdown rendition (produced with
  [markitdown](https://github.com/microsoft/markitdown)) of the `.xlsx` below.
- `deliverables/Survey_Question_Master_List.xlsx` — the same content as the
  source spreadsheet, kept in sync with the `.md` above.

Whenever a newer questionnaire replaces these files, move the outgoing
`Survey_Question_Master_List.*` files into `deliverables/superseded/` first
(don't delete them), then write the new files at the paths above. Older
versions live in `deliverables/superseded/` for history only — never treat
them as current, and never refer to them when answering questions about the
survey.

## Working conventions for Claude

When asked to help in this repo, follow these defaults:

1. **Drafting survey questions**
   - Aim them at validating the talent-development / career-path gap.
   - Keep them answerable by both technical and non-technical staff (or clearly
     tag a question as technical-only when intentional).
   - Prefer a mix of closed (rating / multiple-choice) and a few open-ended
     questions; closed questions make consolidation and analysis easier.
   - Keep language neutral and free of leading phrasing.

2. **Consolidating into Excel**
   - Produce a real `.xlsx` file (e.g. via Python `openpyxl`/`pandas`) so it
     opens cleanly in Excel — not just a CSV unless asked.
   - Suggested columns for the master question list:
     `No. | Contributor | Question | Type (Rating/MCQ/Open) | Audience
     (Technical / Non-technical / Both) | Theme | Notes`
   - One question per row; keep contributor attribution so duplicates and
     overlaps are easy to spot and merge.
   - Save deliverables at the repo root (or a `deliverables/` folder) with clear,
     dated filenames.

3. **General**
   - This repo currently has no build, test, or lint tooling — don't assume any.
   - If a Python script is needed for the Excel step, keep it self-contained and
     note any dependencies (`openpyxl`, `pandas`).

## Status

Early stage: repository initialized. Survey questions are still being collected
from contributors before the master Excel consolidation is built.
