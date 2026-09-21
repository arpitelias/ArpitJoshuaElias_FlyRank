# How to add the next case study

**Arpit Joshua Elias** | General AI Fluency capstone
**Site:** https://arpitelias.github.io (repo: arpitelias/arpitelias.github.io)
**Reminder:** Google Calendar, last Tuesday of every month, 10:00. First one: 29 September 2026.

## Where it goes

`index.html`, as a new section after "Checking the data before trusting the model" and before "How I check data now". Each case is a `<hr>`, an `<h2>` title, a few `<p>` paragraphs, an optional `<figure>` with a real capture, and a closing `<p class="muted">` saying what the case is and isn't.

Images go in the repo root next to `index.html`, named `case-<something>.png`, with `width`, `height` and `alt` set on the `<img>` tag.

## Steps

1. **Open the Portfolio Build Claude Project.** It already holds my proof statement, voice card, identity kit and style note, so drafting is a conversation rather than a rebuild. Check the instructions are in the instructions field and not the description, which has caught me twice.
2. **Get interviewed, not written for.** Ask it to interview me about the piece one question at a time until the problem, my decisions and the outcome are clear, and to push on what I did not do.
3. **Draft in the three beats from Week 2:** the problem, what I did, what came of it. Then a short scope note on what the case does not show.
4. **Run the claims auditor over the draft** before publishing. Put the draft in `C:\mcp-demo\claims-auditor\drafts\` and run `Audit drafts/<file>` in the Claims Auditor project. Fix anything OVERSTATED or UNSUPPORTED. If it flags something true that my claims file does not cover, add it to the claims file at the right tier rather than softening the audit.
5. **Take real captures** of any numbers the case relies on, cropped tight, light mode.
6. **Edit `index.html` on GitHub**, add the section and upload the images, commit to main.
7. **Check it on my phone** in a private tab after two minutes, and click every link in the new section.

On months with no new case: open the site on my phone, fix anything stale, and check the booking link and contact form still work.

## The next piece: the claims auditor

**Problem.** My job-search pipeline checked CVs with a script that matched strings against a file of what I can evidence. It could not tell that "led data quality work" overstates "escalated one issue", because the words differ and the scope is the whole problem.

**What I did.** Built an agent on a Claude Project with a filesystem connector that reads a draft and the claims file from disk and gives every claim one of four verdicts, quoting the sentence and the evidence line. It never rewrites anything. Five test cases were written before building.

**What came of it.** Its second run flagged a sentence I expected to pass. The agent was right: my claims file did not contain the refund incident at all, the story my whole portfolio is built on. I fixed the data, not the agent, and all five tests passed on the third run.

**Scope note.** One user, one claims file, five tests. It checks a document against the file. It cannot check the file against reality.

Source material: `work/fl06_agent_design_spec.md`, `work/fl07_build_log.md`, and the raw run capture.
