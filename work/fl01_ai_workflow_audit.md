# FL-01: AI Workflow Audit and Tool Setup

Arpit Joshua Elias | General AI Fluency, Week 1

## Context

MSc Artificial Intelligence, National College of Ireland. Thesis submitted, viva pending, finishing end of August 2026. Working part-time as a sales assistant in Greystones, Friday to Monday. Tuesday to Thursday are study days. Currently on the FlyRank ML internship and job hunting for AI and data roles in Ireland.

## Workflow Audit

| # | Task | Classification | Rationale |
|---|---|---|---|
| 1 | Viva preparation: re-reading thesis, anticipating examiner questions | Just me | I am being examined on whether I understand my own work, cold, in a room. Rehearsing with AI risks learning to recognise good answers instead of producing them. |
| 2 | Shop floor work at SuperValu Greystones (Fri to Mon) | Just me | Physical, in-person, customer-facing. Nothing to delegate. |
| 3 | Cooking after shifts | Just me | I want the break from screens, and I already know what I am making. |
| 4 | Trekking and days out with college friends (Bray Head, cliff walk, bowling) | Just me | The point is the people and being outside. |
| 5 | Bus commute to Greystones | Just me | Fixed. AI cannot shorten it. |
| 6 | FlyRank internship notebooks: running pipelines, writing analysis | Collaborate with AI | I decide what to test and what the numbers mean. AI helps with pandas syntax and catching things I have missed. Judgement stays mine. |
| 7 | FlyRank written sections: research questions, claim discipline | Collaborate with AI | AI is good at tightening wording, but the observations have to come from what I actually found in the data. |
| 8 | Debugging code errors | Delegate with review | Fast at reading stack traces. I check the fix makes sense before running it. |
| 9 | Understanding unfamiliar ML concepts for the internship | Collaborate with AI | Back-and-forth explanation is what it is best at. I verify against the docs. |
| 10 | Interview preparation for upcoming applications | Collaborate with AI | Practising answers out loud with follow-up questions is useful. The answers still have to be mine and true. |
| 11 | CV, resume and LinkedIn work | Delegated to a person | Already outsourced to someone I hired who knows the Irish market. Worth noting the audit is not only about AI, it is about where work should sit. |
| 12 | Job applications once the CV is ready | Delegate with review | Tailoring cover letters per role is repetitive. Every one gets read before it goes out. |
| 13 | Summarising papers or documentation I need to skim | Delegate with review | Genuinely faster. I read the original if anything matters. |
| 14 | Formatting notes, tables and markdown | Fully automate | Zero judgement involved. |
| 15 | Boilerplate code: imports, setup cells, file paths | Fully automate | Repetitive, easily verified by whether it runs. |

Five tasks are marked "just me". The viva is the one I want to single out. It is not that AI could not help; it is that help would undermine the thing being tested.

## Three Target Tasks for FL-02 to FL-04

**1. Internship analysis notebooks.** Done well means the notebook runs top to bottom without errors, every claim in the markdown is backed by a number in a code cell beside it, and the language stays observational rather than causal. Measurable: zero error outputs, every markdown claim traceable to a printed number.

**2. Interview preparation.** Done well means I can answer a question about my thesis or a project without a rehearsed script, and I can say what I do not know. Measurable: I can explain any section of my thesis in two minutes without notes.

**3. Tailored job applications.** Done well means each cover letter names something specific about the role that is not in the job title, and nothing in it is untrue about my experience. Measurable: no two letters share a paragraph, and I would stand over every sentence in an interview.

## Tool Setup

- Claude: active, with a configured Project (screenshot: `fl01claude_project.png`)
- ChatGPT: free account created
- Anthropic Academy: enrolled in AI Fluency: Framework & Foundations, module 1 complete (screenshot: `fl01academy_enrolment.png`)

### Claude Project custom instructions

> I'm Arpit, finishing an MSc in Artificial Intelligence at National College of Ireland. Thesis is submitted, viva pending, done by end of August. I work part-time as a sales assistant in Greystones, Friday to Monday, so Tuesday to Thursday are my study days.
>
> I'm currently doing the FlyRank ML internship, working through applied ML on search data. I'm also job hunting for AI and data roles in Ireland.
>
> How I like to work: short, direct answers. No preamble. Code with no comments and no unnecessary blank lines. Don't use em dashes. If something I've said is wrong, say so plainly rather than hedging.
>
> Tell me when a task is one I should do myself. I'd rather be told to go and think about something than handed a polished answer I didn't earn. This matters especially for viva prep and anything I'll be examined or interviewed on.
