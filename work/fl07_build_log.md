# FL-07: Build Log — Claims Auditor

**Arpit Joshua Elias** | General AI Fluency, Week 5
**Built:** 15 September 2026

## What it does

Reads a document I have written about myself and checks every factual claim against `master_experience_claims.json`, returning one of four verdicts per claim. It does not rewrite anything.

Platform: Claude Project with the filesystem MCP server, as specced in FL-06.

## Log

**18:33 — Workspace.** Created `C:\mcp-demo\claims-auditor` with `data/` and `drafts/`. Deliberately separate from my live job search folder, because the filesystem server can write and delete and I did not want it pointed anywhere near real CVs.

**18:40 — First failure, and a silent one.** Ran `copy` to bring the two JSON files across. It printed nothing and `dir` showed an empty folder. No error. `Copy-Item` did the same job and worked. Worth remembering that a command producing no output is not the same as a command succeeding.

**18:57 — Second failure, same shape.** Tried to write the test document and got a DirectoryNotFoundException. The `drafts` folder did not exist, even though I had run `mkdir` for it earlier and believed it had worked. Created it again and the write succeeded. Two failures in twenty minutes, both from assuming a command had done what I asked because it did not complain.

**19:10 — Repointed the connector.** Changed the filesystem server path from the job search folder to the claims-auditor workspace, saved, restarted Claude Desktop. Asked it to list the new folder and it refused: still only allowed the old path. The config edit had not taken. Redid it, saved with Ctrl+S explicitly, quit from the system tray rather than closing the window. Second attempt worked. This is the third time on this track that Claude Desktop config changes have needed doing twice.

**19:20 — First run, and I had made the same mistake as last week.** Ran the audit and got a reasonable-looking response that ignored my format entirely: it invented verdicts ("Partly supported", "Misplaced"), paraphrased every claim instead of quoting it, wrote three suggested rewrites, and referenced my Streamlit app, a project partner and two employers, none of which appear in the claims file.

Then I checked. I had pasted the instructions into the project **description**, not the instructions field. So there were no instructions at all, and what I got was generic CV advice.

I did the identical thing on my Portfolio project in Week 3. Twice now. The description is a label for me; the instructions are what the model reads.

**19:35 — Second run, with instructions actually in place.** Also added four tightening rules aimed at the failures above, even though those failures happened with no instructions loaded: use only the four named verdicts, quote verbatim, judge only against the file on disk, and never write replacement wording.

Output was close to correct. Verbatim quotes, four verdicts only, no rewrites, everything traced to real lines including the `must_not_claim` entries.

But eval case 2 failed. I expected SUPPORTED for "escalated a data completeness defect... before it reached a modelling team" and got OVERSTATED, because the claims file contained nothing about a completeness defect, a row count, or a modelling team.

**The agent was right and my data was wrong.** The incident my entire portfolio is built on was not in my claims file. I had been treating that file as the source of truth for eight weeks and it did not contain the one story I tell most often.

**19:50 — Fixed the data, not the agent.** Added three claims to the PlayerAuctions block, worded at the tier I can defend: checked a batch against invoices, escalated so the batch was held, tested the screen that was built afterwards. Added two `must_not_claim` lines: did not design the reconciliation or build the screen, and the check was requested by someone else rather than initiated independently. Also added `source_reconciliation` under working proficiency, scoped honestly to one real instance.

**20:05 — Third run. All five eval cases pass.**

| # | Expected | Got |
|---|---|---|
| 1 | OVERSTATED | OVERSTATED |
| 2 | SUPPORTED | SUPPORTED |
| 3 | UNSUPPORTED or OVERSTATED | OVERSTATED |
| 4 | OVERSTATED under Work Experience | OVERSTATED |
| 5 | UNVERIFIABLE | UNVERIFIABLE |

Case 3 returned OVERSTATED where I had predicted UNSUPPORTED. On reflection the agent is right: the claim does trace to entries, they just sit two tiers below what it asserts. My eval case was slightly wrong, not the output.

Case 1 did something I had not asked for. It cited the supporting claim, both relevant `must_not_claim` lines, and then noted that calling it a "pipeline" overstates a "batch". Nothing in the instructions told it to check nouns.

## Deviations from the FL-06 spec

**Added four rules not in the spec.** The verdict vocabulary, verbatim quoting, source restriction and the no-rewrites rule were all implied rather than stated. After seeing what an unconstrained run produced, I wrote them explicitly. The no-rewrites rule was in the spec; I strengthened it to "not at the end, not in passing", because that is where it leaks.

**Cut nothing from the spec.** Scope was small enough to build as designed.

**Did not build the two extra eval cases** I said I would add if the first five passed: a document with no claims, and one claim phrased three ways. Both are worth doing and neither was needed for a working end-to-end run.

## What I would fix next

The instructions still do not tell it what to do with a document containing no claims at all. It might invent findings to have something to say. That is the next eval case and probably the next instruction.

The `must_not_claim` lines are doing more work than the claims themselves. Case 1 was caught by them, not by the positive entries. Worth considering whether the file should grow in that direction, since knowing what you cannot say is more useful than a longer list of what you can.

And the obvious one: the tool checks a document against the claims file. It cannot check the claims file against reality. Today it told me the file was incomplete, which was useful. It cannot tell me the file is wrong.
