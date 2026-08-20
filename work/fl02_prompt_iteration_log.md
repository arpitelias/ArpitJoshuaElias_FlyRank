# FL-02: Prompting Fundamentals on Real Tasks

**Arpit Joshua Elias** | General AI Fluency, Week 2

## The task

Interview preparation. This is target task 2 from my FL-01 workflow audit, classified there as "collaborate with AI": practising answers with follow-up questions is useful, but the answers have to be mine and true.

All six versions were run in logged-out ChatGPT, in a fresh window each time, so no memory or account history could contaminate the comparison. My first attempt at a baseline was run in Claude and had to be discarded: it returned detailed knowledge of my background from a five-word prompt, which meant the baseline was already at roughly version 3 quality. That is worth recording as a finding in itself. A prompt ladder is meaningless if the tool already knows you.

---

## Version 0: naive baseline

**Prompt:** `Help me prepare for my interview`

**Output:** A numbered list of five things it needed from me (job title, interview type, date, background, what worries me), followed by a menu of seven things it could then help with.

**Notes**
- *Technique:* none, this is the baseline.
- *What changed in the output:* n/a.
- *What failed:* it produced no preparation at all. A reasonable response to a five-word prompt, and useless.
- *What next:* give it a role, so it has a point of view rather than a service list.

---

## Version 1: role assignment

**Technique:** role assignment.

**Added:** "You are an experienced hiring manager for data and AI roles in Ireland. You have run hundreds of interviews and you know what separates a candidate who gets an offer from one who interviews adequately."

**Notes**
- *What changed in the output:* it stopped listing services and started stating standards. It set an objective ("the interviewer thinks: I want this person on my team"), named eight capabilities it would assess including data quality, knowing when not to use ML, and communicating to non-technical people, and committed to challenging weak answers rather than improving them. It also told me not to give it polished answers first, which is a hiring manager instinct rather than a coaching one. The baseline was a menu. This had a view.
- *What still failed:* it asked for the same five inputs and produced no preparation. A role tells it how to think, not what it is thinking about.
- *What next:* give it the context it keeps asking for.

---

## Version 2: context and motivation

**Technique:** context and motivation.

**Added:** my actual position (MSc pending viva, operations background, applied ML internship, targeting data governance in pharma), the gap in my experience (no production ML, never shipped a model), and why the differentiator matters: I am competing against candidates with the same degree and more relevant experience, and my only real edge is having seen data where it is created.

**Notes**
- *What changed in the output:* it stopped requesting inputs and started preparing. It produced 33 role-specific questions grouped by type, identified ALCOA+ as table stakes for pharma, and gave me a non-bluffing answer for the production ML gap. Most tellingly, it named "tell me about a data problem you saw in operations" as the single question that would differentiate me, which is a direct read of the motivation paragraph rather than generic advice.
- *What still failed:* far too long to use under pressure. It proposed a mock interview but never started one. And it invented an illustrative example, an operator miscategorising records, which is not from my experience.
- *What next:* give it a real example so it stops inventing them.

---

## Version 3: few-shot example

**Technique:** few-shot examples.

**Added:** one worked example from my operations experience, the 400,000-row sales batch where refunds had not been entered, including explicitly what I did not do (I found the error but did not design the reconciliation or build the screen).

**Notes**
- *What changed in the output:* it stopped inventing scenarios and worked entirely from my actual case. It derived the validation vs reconciliation distinction from the example, with a worked table showing rows that pass every field-level check while the dataset is still incomplete against source. It generated four adversarial follow-ups aimed at my specific story, including "how did you know the invoices were the right source of truth?" It also picked up my "I did not build the screen" line and turned it into a section warning me against overselling, listing what I did and did not do side by side.
- *What still failed:* around 3,000 words across seventeen numbered sections with no priority order. Still advice about practising rather than practice.
- *What next:* constrain the structure so the output is usable.

---

## Version 4: output structure

**Technique:** output structure.

**Added:** a fixed four-part format (90-second answer, five hardest questions with what each tests, three things never to claim, one thing to learn) and a 600-word ceiling.

**Notes**
- *What changed in the output:* it stopped explaining and started producing. The "tell me about yourself" answer is written to be said aloud rather than described. Version 3 gave 33 questions with no ranking; this gave five with a line on what each one actually tests, which is the part I could not have worked out alone. Around 500 words against 3,000.
- *What still failed:* one real loss. Version 3's four story-specific hostile follow-ups are gone. They were the most useful output on the ladder and the word limit killed them.
- *What next:* stage the task so depth survives the structure.

---

## Version 5: step decomposition

**Technique:** step decomposition.

**Added:** four labelled stages with a per-stage word limit and an explicit instruction not to merge them, including a dedicated stage for follow-ups on my specific example.

**Notes**
- *What changed in the output:* it recovered what compression had cost. The story-specific follow-ups are back as their own stage with answers attached. Stage 2 also produced a harder question set than any earlier version, including "why shouldn't we hire someone with three years of governance experience?", which no previous version asked. Per-stage limits protected depth that a single global limit had crushed.
- *What failed:* the 90-second answer got worse. Version 4 said plainly "I didn't build that control, so I wouldn't claim that I did." Version 5 softens this to "the process was subsequently strengthened", which is passive and hides who did what. The honesty survived in stage 4 but leaked out of the part I would actually say aloud.

---

## Cross-model comparison

I ran the final version 5 prompt on both ChatGPT and Claude.

**One caveat first.** The Claude run was not clean. It opened by saying it had read my job-search notes and referenced things that were not in the prompt: ML keywords on my CV, a GitHub placeholder. Claude had memory or project context available and used it. That is not a fair comparison, and it is the same contamination that forced me to discard my first baseline. It also produced Claude's single best question, so the contamination helped the output while invalidating the test.

**Claude was more adversarial.** ChatGPT's follow-ups let me look competent: how did I know the invoices were authoritative, why wouldn't a standard check have caught it. Claude asked "why hadn't you flagged the absence of a source reconciliation before anyone asked?" and "how far off was it, in euros or percent?" The first has no flattering answer available. The second is a question I currently cannot answer, which makes it the most useful thing either model produced.

**Claude gave regulation, ChatGPT gave direction.** ChatGPT said to learn ALCOA+ and GxP fundamentals. Claude named EU GMP Annex 11, 21 CFR Part 11 and the MHRA data integrity guidance, and suggested building a small artefact with expectations written against a dataset as if for an auditor. One is a topic, the other is a reading list and a deliverable.

**ChatGPT kept the honest line where it mattered.** Claude's Stage 1 is a better spoken answer overall, more specific about what the operations job actually involved, but it never mentions that I did not build the control. Stage 4 states it forcefully. ChatGPT's version 4 put it directly into the 90-second answer, which is the only place it gets said out loud.

**Neither respected the per-stage word limits.** Both ran well over 250 words per stage. The instruction shaped the structure but not the length.

**Where Claude overreached.** It wrote suggested answers to the follow-ups, including a specific claim about how I performed the reconciliation: aggregate totals by period, then drill down into affected transaction types. I never told it that. If I repeated it in an interview and it was not what happened, that is exactly the verifiable overclaim it warned me about two sections later. The more confident model produced the more dangerous output.

---

## Final reusable template
---

## What I learned

The layer that changed the most was the worked example. Before it, both models invented scenarios to illustrate their points. After it, everything was about my actual case, and one model built a whole conceptual distinction out of it.

Including what I did *not* do was worth more than anything I claimed. Both models picked it up and turned it into advice about credibility, and both independently warned me that a single verifiable overclaim contaminates everything else I say.

The thing I will carry forward is that structure and depth trade against each other, and staging is how you get both. A single global word limit forced the model to drop its best material. The same limit applied per stage kept it.
