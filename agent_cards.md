# Agent cards: every prompt for the practical, ready to copy

*Agents for Analysts, part 2 (KAPSARC, 17 November 2026). Open this file on a second laptop at https://github.com/alesmarsal/agents-for-analysts/blob/main/agent_cards.md (GitHub puts a copy button on every prompt) and copy each card into Claude Code (or Cowork, where it says so). Card numbers match the activity numbers on the slides. After Activity 6 the file is also in your data\raw folder.*

**The case.** Why do OPEC, the IEA and the EIA disagree about world oil demand in 2026? In the September 2026 editions, 2026 demand is OPEC 105.8 mb/d, EIA 102.6 and IEA 102.4 (IEF comparison, 14 Sep 2026, p. 3).

**Roles at every table.** Driver types at the team laptop. Navigator reads the card aloud, adapts it, and explains what the agent did. Checker opens the source on a second laptop and checks the numbers, touching nothing. Rotate the Driver after every activity.

---

## Card 5. One folder, two agents (2 minutes)

PowerShell:

```
mkdir ~\projects\oil-agents
```

Desktop app → **Cowork** → **Add folder** → `oil-agents`, then ask Cowork:

```
Create README.md with one line: "This project asks why OPEC, the IEA and the EIA disagree about world oil demand in 2026."
```

PowerShell:

```
cd ~\projects\oil-agents
claude
```

Then ask Claude Code:

```
Read README.md and tell me in one sentence what this project is about.
```

---

## Card 6. Get the data, then write the project's CLAUDE.md (6 minutes)

**Navigator, in the browser:** open https://github.com/alesmarsal/agents-for-analysts (or scan the code on the slide) → green **Code** button → **Download ZIP**. It lands in Downloads as `agents-for-analysts-main.zip`. GitHub blocked or no network: copy `agents-for-analysts-main.zip` from the USB stick into Downloads.

Do not unzip it yourself: Windows' *Extract All* puts the files one folder too deep, and every path on these cards breaks.

**Card 6a. Driver, in Claude Code:**

```
Unzip the newest agents-for-analysts zip in my Downloads folder into data/raw, with no subfolder: data/raw/README.md must exist. Then download the two IEF PDFs listed in data/raw/manifest.csv into data/raw, under the file names given there. If a download is blocked, stop and tell me.
```

If the IEF download is blocked: the Navigator opens the two IEF links in `data\raw\README.md` in the browser and saves each PDF into `data\raw` as `2026-09_IEF_comparison.pdf` and `2026-02_IEF_comparison.pdf`. The IEF does not allow reposting, so these two files are not in the pack or on the USB stick.

Checker: open `data\raw\2026-09_IEF_comparison.pdf`. Does page 1 say September 2026?

**Card 6b. Driver, in Claude Code:**

```
Create the folders data/derived, notes, code, output and logs. Then write CLAUDE.md, at most 25 lines: the question from the README.md in this folder, where things live, and these rules: data/raw is read-only; every number carries its file and page; write "not in source" rather than guess; on Windows run Python as py; ask before deleting anything. Show it to me before saving.
```

Checker: find every rule in CLAUDE.md.

---

## Card 7. Turn two reports into notes with page numbers (7 minutes)

```
Read data/raw/2026-09_IEF_comparison.pdf. Write notes/ief_2026-09.md: a table of world oil demand by OPEC, the IEA and the EIA for 2025, each quarter of 2026 and 2026, with the PDF page of every number. Then three bullets on how the IEF explains the differences, with pages. Copy numbers exactly; write "not in source" if a number is missing.
```

Then:

```
Do the same for data/raw/reports/2026-09_EIA_STEO.pdf, using Table 3a (PDF p. 33). Write notes/eia_steo_2026-09.md.
```

Checker: open the PDF page and check two numbers in each note. Navigator: do the IEF's EIA numbers match the EIA's own?

---

## Card 8. Plan the answer in plan mode (5 minutes)

Press `Shift+Tab` until the line under the input box says *plan mode*. Then:

```
Using only notes/, data/raw/excerpts_OPEC_IEA.md and data/raw/gdp_note.md, plan how to answer: why do OPEC, the IEA and the EIA disagree about world oil demand in 2026? Give at most five sub-questions. For each: the data, the source file and page, and the output (one table or one chart). Do not compute anything yet.
```

Navigator drops or adds one sub-question. Then leave plan mode (`Shift+Tab`) and ask:

```
Save this plan as plan.md.
```

---

## Card 9. Build your first skill, then use it (8 minutes)

**9a. Build it.** Paste this whole block:

```
Create .claude/skills/extract-with-evidence/SKILL.md with exactly the text below. Show it to me before saving.

---
name: extract-with-evidence
description: Extract numbers from source files into a table with evidence. Use whenever numbers are taken from reports.
---
1. Read only the files named in the task.
2. Write a CSV with the columns agency, metric, period, value, unit, file, page, quote.
3. Copy each number exactly as printed.
4. Missing? value NA and quote "not in source".
5. Compute nothing in this step.
```

**9b. Use it.**

```
Use the extract-with-evidence skill on notes/ and data/raw/excerpts_OPEC_IEA.md. Build data/derived/forecasts_2026.csv: world oil demand for 2025, each quarter of 2026 and 2026, for OPEC, the IEA and the EIA.
```

If Claude Code does not find the new skill, type `/exit` and start `claude` again in the same folder.

Checker: pick three rows at random and open each page.

---

## Card 10. An analyst, a checker, and you as the judge (10 minutes)

**10a. Create the two agents.** Paste this whole block:

```
Create two subagent files with exactly the text below, then list them.

File .claude/agents/analyst.md:
---
name: analyst
description: Builds tables and charts from data/derived with a script that can be rerun. Use for every computation step.
tools: Read, Write, Edit, Bash, Glob, Grep
---
1. Read plan.md and the input file you are given.
2. Write one script in code/ that reads data/derived/ and writes to output/.
3. Use the Python standard library only; on Windows run it with py.
4. Run it, and check that the output exists and has the expected rows.
5. Never edit data/raw/. Report the files you wrote.

File .claude/agents/checker.md:
---
name: checker
description: Independent checker. Recomputes numbers from the sources and compares. Use after every analysis step.
tools: Read, Write, Grep, Glob, Bash
---
You edit nothing except output/check_report.md.
1. Without opening code/ or output/, recompute the numbers from notes/ and data/raw/.
2. Then compare with the analyst's output/ files.
3. Write output/check_report.md: one row per number, PASS or FAIL, and the difference.
4. End with VERDICT: PASS or VERDICT: FAIL.
```

Check with `/agents`. If the new agents do not appear, type `/exit` and start `claude` again in the same folder.

**10b. Run them.**

```
Act as orchestrator. Run the analyst: from data/derived/forecasts_2026.csv build output/gap_table.csv (the OPEC-IEA and OPEC-EIA gaps for 2025, each quarter of 2026 and 2026) and output/gap_chart.svg, with a script in code/. Python standard library only; run it with py. Then run the checker. If it fails, send it back to the analyst once, then report to me.
```

Checker (human): verify one FAIL, or one PASS, by hand from the PDF. Navigator: explain the chart in one sentence.

---

## Card 11. Write the state, wipe the memory, recover (4 minutes)

```
Write logs/STATE.md: objective, done, in progress, next step, decisions, open questions. Append one dated line to logs/progress.md.
```

Type `/clear`. Then:

```
Read CLAUDE.md and logs/STATE.md. Where are we, and what is the next step?
```

Stretch:

```
Which choices did you make today that I did not ask for?
```

---

## Card 12 (stretch). The 150-word answer

```
Only if output/check_report.md says PASS: write output/brief.md, at most 150 words, answering why OPEC, the IEA and the EIA disagree about world oil demand in 2026. Use only numbers from output/ and notes/, each with its source and page. End with one sentence on what we did not check.
```

Then:

```
Use the checker agent to check every number in output/brief.md against its source.
```

---

## Stretch: make the raw-data rule unbreakable

```
Create .claude/settings.json that denies any edit inside data/raw. Then try to edit data/raw/gdp_note.md and tell me what happened.
```
