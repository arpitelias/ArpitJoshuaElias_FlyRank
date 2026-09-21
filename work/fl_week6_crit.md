# Survive the Crit

**Arpit Joshua Elias** | General AI Fluency, Week 6
**Site:** https://arpitelias.github.io

## What I gave the reviewer

The live URL, the two questions to answer from the top of the page before scrolling, and my proof statement placed at the end of the message so his first impression was not my claim read back to him:

> I catch bad data before it turns into a confident wrong answer, and I'm trying to convince a data governance lead at a pharma company to book a 15 minute call with me.

The reviewer is a friend who had not seen the site before. He wrote his feedback himself and used an AI tool to tidy the wording. I mention that because two of his points were factually wrong in a way that looks like it came from the tidy-up rather than from looking at the page. I have treated those as "checked, not changed" below rather than quietly dropping them.

## Round 1 feedback (verbatim)

**1. In one sentence, what do I do?**
You catch silent/bad data (the kind that looks fine in the file) before it turns into a confident wrong answer downstream.

**2. Would you believe I'm good at it? Why or why not?**
Partially. The top is clean, specific, and avoids the usual AI/data-science word salad. Ops background + MSc AI is a plausible combination for this exact problem. But the top is pure claim with zero proof, so belief is provisional at best — I'd need the rest of the page to decide.

**What works**
- The core story is concrete and lands the exact point you're selling: missing refunds left no trace, validation rules wouldn't catch it, the model would have run clean and confident. That's the right example for a data-governance audience.
- You own the limits of the story ("I didn't design the reconciliation and I didn't build the screen"). That honesty is better than the usual inflated ownership.
- The positioning in About is sharp: operations is where the errors are born; most model people only ever see cleaned warehouse data. That's a real differentiator.
- Clear, low-friction CTA and you explicitly name the target (data governance / data quality, ideally pharma).

**What felt off / weakened the case**
- The story is mostly "someone asked me to check, I noticed the totals were high, I escalated." That's useful, but it's not especially high-skill or systematic. A data-governance lead will read it as "good instinct + willingness to push back," not "this person systematically finds and prevents these failures." You found a gap that shouldn't have existed; you didn't invent a new control.
- Zero evidence of repeatability. One anecdote from (apparently) a previous ops role is thin. No second example, no metrics (how big was the error in €/%, how many similar issues did you catch, what did the screen actually catch after you tested it?), no process you now run by default.
- "Writing" section is empty ("First posts going up shortly"). Empty sections look like unfinished work. Kill it or put one real note up.
- Site itself is extremely bare. Plain GitHub Pages text is fine for minimalism, but for someone pitching data quality/governance it undercuts the message a bit — there's no visual hierarchy, no proof points, no links to anything else (LinkedIn, GitHub projects, code, previous work). It feels like a one-page note rather than a professional presence.
- Pharma angle is stated only at the bottom. The story is sales/advertising data. A pharma data-governance lead will immediately wonder whether you understand regulated data, audit trails, GxP, etc. The site doesn't bridge that gap at all.
- "I finished an MSc in Artificial Intelligence at National College of Ireland in 2026." Depending on the exact date this is read, that can read as either just-finished or still-in-progress. Either way it's very recent, so the practical experience weight is almost entirely on the ops side.
- The "Send" at the bottom looks like a non-functional placeholder in the text extract (no visible form fields or confirmation). If the form actually works, fine; if it doesn't, that's an immediate drop in credibility.

**Net effect on booking a 15-minute call**
I'd book the call if I already had the problem and was actively looking, because the problem framing is good and the ask is low-risk. I wouldn't go out of my way or forward it aggressively. It currently proves "I noticed a real silent data error once and escalated" more than "I systematically catch bad data before it becomes a confident wrong answer." For a data-governance lead in pharma, the evidence bar is higher than one ops anecdote + a recent MSc.

Stronger version would need either (a) one more concrete example with clearer ownership/impact, or (b) a short description of the actual method/checklist you now use so it doesn't feel like a one-off.

## How I sorted it

The test for must-fix: confusing, broken, hurts the one action, or the proof does not land.

**Must-fix**

| Feedback | Why it is must-fix | What I changed |
|---|---|---|
| One anecdote, no evidence of repeatability | The proof does not land. He believed I had good instinct, not that I have a method, which is the whole claim | Added a second case study from my FlyRank internship: checking a 9.8 million row dataset before modelling, deliberately breaking a model to see what a leak looks like, and later catching my own label definition fixing a fifth of the data at zero. Two real notebook captures included |
| No process I run by default | Same failure: without it the cases read as one-offs | Added "How I check data now", four rules drawn from what I actually did in both cases |
| Pharma angle never bridged | Hurts the one action. My target reader would wonder immediately and there was nothing to answer them | Added a paragraph in About: my thesis worked with GMP-compliant pharmaceutical manufacturing data, stated as academic exposure, and a plain statement that I have not worked in a GxP environment |
| Empty Writing section | Reads as unfinished, which undercuts a site about noticing what others miss | Removed it until there is a real post |
| Ambiguous MSc line | Confusing about my actual status | Now reads "completed" |

**Nice-to-have**

| Feedback | Why it waits |
|---|---|
| Size of the refund error in € or % | I do not remember the figure and will not invent one. Leaving it out is more honest than a guess |
| More visual hierarchy | A real point, but a design pass, not something stopping the reader believing me |
| (Round 2) A headline clause nodding at my own models | He marked it not required. The headline is the claim I chose in Week 3 and loading more onto it would cost the thing that makes it memorable |

**Checked, not changed**

| Feedback | What I found |
|---|---|
| No links to LinkedIn or GitHub | Both are in the footer, alongside the CV and booking link |
| Send button looks like a non-functional placeholder | The form works. I tested it live on 21 September and the submission reached my inbox |

I asked him in my reply whether either had failed to show on his device, rather than assuming he was wrong.

## Round 2 feedback, after the changes (verbatim)

**1. In one sentence, what do you do?**
You catch bad/silent data problems before they turn into confident wrong answers.

**2. Would I believe you're good at it?**
Yes, more than before. The line is still clean and specific, and "Operations background + MSc AI" still feels like a credible combination for this exact problem. Nothing at the top overclaims. Belief is still provisional until the evidence sections, but the framing itself no longer feels like pure assertion.

The rest of the page is substantially stronger. The second case (9.8M rows, the 36.7% availability filter, deliberately leaking a feature to get AUC 1.000, then catching your own label definition that forced 17k pages to zero) is concrete, self-critical, and shows method rather than just instinct. The four-point "How I check data now" section is the biggest upgrade — it turns the stories into a repeatable approach. The pharma/thesis paragraph is honest and well-calibrated.

One small note on the top itself: it still leads with the same two lines. That's fine — they're good — but if you ever want the top to carry a bit more of the new weight, a single extra clause could help (e.g. something that nods at "including my own models"). Not required.

Overall the site now does what you said it needs to do.

## What I took from it

His first answer to "what do I do" was already right, so the claim was never the problem. The problem was that I had one story and was asking it to prove a habit. I had the evidence for a habit the whole time, in eight weeks of notebooks, and had not thought of it as portfolio material because it was internship work rather than a job. The fix was mostly moving what I already had to where the reader could see it.
