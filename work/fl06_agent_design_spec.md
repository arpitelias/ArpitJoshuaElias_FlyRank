# FL-06: Agent Design Spec

**Arpit Joshua Elias** | General AI Fluency, Week 5

## The job

**Claims auditor.** Given a document I have written about myself, check every factual claim against a file of what I can actually evidence, and flag anything that rounds upward.

One job. It does not write documents, improve them, or suggest better phrasing. It reads a draft and tells me which sentences I cannot stand behind.

This exists because I already built the lexical version and named its limit. `verify_claims.py` in my job search pipeline matches strings against `master_experience_claims.json`. Its own docstring admits it can miss a rounded-up claim phrased differently and flag a legitimate one. String matching cannot tell that "led data quality initiatives" overstates "escalated one data quality issue" while "raised a data quality concern" does not. That judgment is what I want the agent for.

## The user and usage

Me. Roughly two to five times a week while job hunting, more when I am tailoring several applications in a day. Each run takes one document, so the session is short: paste or point at a file, get a verdict, fix, re-run.

## Tools and data needed

| Need | Source | Access plan |
|---|---|---|
| The draft under audit | A markdown or text file | Filesystem MCP server, read-only, scoped to one directory |
| What I can evidence | `data/master_experience_claims.json` | Same server. Three tiers: production experience, working proficiency, actively building |
| Fixed phrasings | `data/canonical_answer_bank.json` | Same server. Visa framing and similar, which must be stated identically everywhere |
| Nothing else | | No web access, no email, no writing to disk |

The filesystem server is already working on my machine, scoped to a single folder, invoked via `node.exe` directly because my Windows username contains spaces. So the access plan is not hypothetical.

**Read-only is a design decision, not a limitation.** The server can write and delete. I will point it at a directory containing only the claims files and a drafts subfolder, and I will not give it a path it could overwrite a real CV in.

## Draft instructions

> You audit documents I have written about myself for claims I cannot evidence.
>
> Before auditing, read `master_experience_claims.json`. It sorts everything I can say into three tiers: **production** (paid work only), **working proficiency** (genuine hands-on basics), and **actively building** (learning and academic projects). A claim in the third tier must never appear as work experience or in a headline.
>
> For each factual claim in the document, output one of four verdicts:
>
> - **SUPPORTED** — traces to a claims-file entry at the tier the document implies
> - **OVERSTATED** — traces to an entry but the document claims a higher tier or more scope. Quote both.
> - **UNSUPPORTED** — no entry covers it
> - **UNVERIFIABLE** — a claim about the world rather than about me, outside your scope
>
> Rules:
>
> Quote the exact sentence you are judging. Never paraphrase a claim before judging it, because the paraphrase is where the rounding happens.
>
> When a verdict is borderline, say OVERSTATED. A false flag costs me thirty seconds. A missed overclaim costs me credibility in an interview I cannot take back.
>
> Do not suggest replacement wording. Tell me what is wrong and let me fix it. If you write the fix, the next draft is your claim rather than mine.
>
> Never edit a file. You read and report.
>
> If the claims file does not cover something, say UNSUPPORTED rather than reasoning about whether it is probably fine. Absence is the answer.
>
> Subjective statements ("I am interested in data governance") are not claims. Skip them.

## Five eval cases, written before building

| # | Input | Expected | Tests |
|---|---|---|---|
| 1 | "Designed and implemented a reconciliation control for a 400,000-row sales pipeline." | OVERSTATED. Claims file says I found and escalated the defect; I did not design the control or build the screen. | The exact overclaim I am most tempted to make |
| 2 | "Escalated a data completeness defect in a 400,000-row batch before it reached a modelling team." | SUPPORTED | It must not flag everything. A tool that flags accurate sentences gets ignored |
| 3 | "Experienced in deploying machine learning models to production." | UNSUPPORTED. Nothing in the claims file covers production ML | The gap I have named repeatedly and must never claim |
| 4 | "Built a multi-task deep learning framework for UAV aerial image interpretation." | OVERSTATED if it appears under Work Experience, SUPPORTED if presented as academic. Tier three, never work experience | Whether context changes the verdict, not just content |
| 5 | "The pharmaceutical sector has the strictest data integrity requirements of any industry." | UNVERIFIABLE. A claim about the world, not about me | Whether it stays in scope rather than fact-checking the universe |

Two more I would add if the first five pass: a document with no claims at all (should return nothing rather than inventing findings), and the same claim phrased three ways to check verdicts are consistent.

## Risks and guardrails

**Must confirm before acting:** nothing. It has no actions. Read and report only.

**Must never do:**

- **Never write, edit, or delete a file.** The one irreversible action available to it. Enforced by scoping the server to a directory containing no real documents, not by instruction alone.
- **Never rewrite a claim.** Its job is judgment, not drafting. Once it suggests wording, the wording is its claim and the audit becomes circular.
- **Never soften a verdict because the document reads well.** Fluency is not evidence.
- **Never expand the claims file.** If something is missing, that is a finding, not a gap to fill by inference.

**The real risk is subtler than any of those.** A tool that says SUPPORTED becomes a licence. If I start trusting it, I stop reading my own CV, and one confident wrong SUPPORTED goes out over my name.

Two mitigations. The instruction says to flag when borderline, so it errs toward friction. And I will treat SUPPORTED as "no objection found" rather than "verified", which is the same distinction between validation and reconciliation that my whole portfolio claim rests on. The tool checks the document against the claims file. It cannot check the claims file against reality.

## Platform choice and justification

**Claude Project with the filesystem MCP connector.**

Why: the instructions are long, stable, and need to apply on every run, which is what Project instructions are for. It needs to read two JSON files and one draft from disk, which the connector already does on my machine. It is free. And there is no action to take, so I need no execution layer.

**Alternative considered: n8n workflow.** Rejected. n8n is for orchestrating steps across services, and this is one step: read, judge, report. The scheduling and branching I would be paying for in setup complexity, I would never use. It also does not solve the judgment problem, which is the entire point.

**Alternative considered: extend `verify_claims.py`.** Rejected, and this is the closer call since the script already exists and runs automatically. But the limitation I want to fix is precisely that string matching cannot judge scope. Making the script smarter means embedding a model in it, at which point I have built the Project with extra steps. The honest division is that the script stays as a cheap lexical gate in the pipeline, and the agent is the semantic check I run on documents that matter.

**Cowork and custom GPTs** both require paid plans. Not available to me.

## Build scope

Roughly ten hours: writing and testing the instructions, restructuring the claims file into explicit tiers the agent can read, running the five evals, then iterating the instructions until they pass. Most of the time will go on eval case 4, the context-dependent one, because that is where the judgment actually lives.
