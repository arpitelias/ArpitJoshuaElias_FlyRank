# FL-04: Ship an Automation Workflow

**Arpit Joshua Elias** | General AI Fluency, Week 4

## The pipeline

Job application preparation. This is target task 3 from my FL-01 audit, classified there as "delegate with review": tailoring an application per role is repetitive, but every one gets read before it goes out.

I built it on 30 August 2026 and it has run daily since. Nine days of real output, 31 tracked roles, 22 tailored application packs.

## Why this task

Before the system, one application meant searching boards by title, reading listings that turned out to be irrelevant, deciding whether the role was worth pursuing, tailoring a CV, writing a cover letter, and preparing form answers. Most of that time went to sourcing rather than writing, and title-based searching kept returning roles that shared a word with what I wanted and nothing else.

The deeper problem is the one in my portfolio claim. Tailoring a CV per role creates constant pressure to round upward. An academic project starts reading as production work, "familiar with" becomes "experienced in", and nobody notices because each individual sentence is defensible. The operating manual I wrote for the system states it directly: it is easier to lie on a CV than to notice you have, and most of the machinery exists to stop that.

## The steps

Five steps with defined handoffs. Steps 1, 2 and 5 are scripted; 3 and 4 are Claude in VS Code working under a written operating manual.

**1. Source.** `jobspy_fetch.py` pulls Indeed and LinkedIn for Ireland, full job descriptions rather than list summaries. `irishjobs_fetch.py` covers IrishJobs.ie and Jobs.ie. Search terms live in one file, `job_filters.py`, derived from a target-roles document. Handoff: raw CSV.

**2. Screen.** Roles are scored on skills overlap, never on title, across eight dimensions: current fit, learnability, interview risk, industry fit, permit fit, career value, location, technical intensity. Handoff: screened CSV. 17,596 raw rows to 12,380 screened.

**3. Select.** I ask for a specific number for that day, usually three strong targets and two stretch. Claude reads the job descriptions and returns them with permit assessment, why it fits, missing requirements and interview risk. Handoff: rows appended to `trackers/applications.csv`.

**4. Tailor.** Per selected role: a role-specific CV in markdown, a cover letter, and a Q&A sheet with verbatim answers for application forms. Handoff: markdown files in a dated delivery folder.

**5. Gate and compile.** `verify_claims.py` checks every CV against `master_experience_claims.json`, which sorts everything I can say into three tiers: production experience (paid work only), working proficiency (genuine basic hands-on), and actively building (learning and academic projects, never allowed under Work Experience or in the headline). Then `compile_docs.py` makes the PDF and `ats_analyzer.py` checks the PDF parses. Handoff: PDF pack in the delivery folder, ready to submit.

A person named Darren submits the applications. The system never claims an application was sent, because it cannot send one.

## Five real runs

| Date | Roles delivered | Examples |
|---|---|---|
| 2026-09-01 | 4 | EirGrid Data and Reporting Analyst, FedEx DT BA, PartnerRe Data Analyst, Carraig Junior BPA |
| 2026-09-02 | 2 | Sanofi Data Integrity Expert, Tuath Data Analyst |
| 2026-09-03 | 3 | Ardonagh Data Analyst, Primark Procurement Data, Robert Walters Governance and Compliance |
| 2026-09-04 | 3 | PM Group Data Integrity, Adaptive HVM Data Analyst, TELUS Legal Quality Analyst |
| 2026-09-05 | 5 | Sandvik Master Data, Uniphar Junior BA Finance, Virtu Trading Ops, eFrontiers Junior BA, ML BA HR Payroll |

Each produced a tailored CV in markdown, a compiled PDF, a cover letter and a Q&A sheet. 22 packs across the five days.

Outcomes so far, from the tracker: 6 applied, 4 rejected, 3 closed before applying, 1 dropped after I found it required a full Irish driving licence, the rest queued or shortlisted.

## Time accounting

**Setup: one full day.** Writing the operating manual, the five scripts, the claims JSON and the answer bank.

**Before: roughly 90 minutes per application.** Searching boards, reading listings that turned out not to fit, deciding, tailoring the CV, writing the cover letter, preparing form answers.

**After: roughly 15 minutes per application of my time.** One instruction naming how many strong and stretch roles I want, then reviewing what comes back. The scripts run unattended.

**Break-even.** At about 75 minutes saved per application, the setup day paid for itself somewhere around application seven or eight. I passed that on day three.

**The honest caveat.** This measures my time, not total time. Darren still submits every application manually, and that has not changed. The system compresses sourcing and drafting, which was the bottleneck for me, and does nothing about submission, which the operating manual itself names as the real bottleneck: sending beats building.

## Where it breaks

**Generated CVs are not ATS-ready first time.** This is the most common failure. The markdown reads well and the PDF compiles, but the parser check flags problems and the CV needs manual tweaking before it will survive an ATS. `ats_analyzer.py` catches it, but catching is not fixing, and the fixing is mine.

**Output quality tracks prompt quality.** Over nine days I kept adjusting how I ask, and the returns changed noticeably. Early instructions produced roles that shared a keyword with my target and little else. Naming the split explicitly, three strong and two stretch, fixed most of it. This is not a bug so much as the system reflecting what I give it.

**The claims gate is lexical, not semantic.** `verify_claims.py` matches strings. It can miss a rounded-up claim phrased differently and it can flag a legitimate one. The script's own docstring says so. A FAIL means delete the PDF and fix the CV, and it does not block compilation, so a human has to read the output rather than trust the exit code.

**Boards lie about dates and employment type.** Listings misreport posting date and permanent versus contract. Both have to be re-derived from the job description text.

**Contacts found by web search are provisional.** Any named person surfaced by search is unverified until confirmed from a live source. This is a rule in the manual because getting it wrong means messaging the wrong person.

## What a human must still check

- **Every claim in every CV.** The gate is a lexical safety net, not a substitute for reading.
- **ATS output.** The parser flags; I fix.
- **Permit and sponsorship assessments.** These are inferences from company size and role type, not confirmed facts. The manual requires verifying at application or offer, and forbids inventing salary or sponsorship.
- **Whether the role is real.** One role reached the pack stage before I noticed it required a full Irish driving licence, which I do not have. No screening rule caught it.
- **Submission itself.** A person applies. The agent builds and queues.

## A note on tooling

The brief suggests no-code tools: a Claude Project, NotebookLM, a custom GPT, n8n. Mine is Claude Code in VS Code with Python scripts, so it is not no-code. I built it before this assignment for real use rather than as an exercise, and I would rather submit the thing that actually runs than rebuild a weaker version to fit the tool list. The workflow requirements are met either way: five distinct steps, defined handoffs, five documented runs, honest time accounting, and named failure points.
