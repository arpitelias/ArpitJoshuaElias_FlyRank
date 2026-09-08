# FL-05: Agent Concepts and MCP Basics

**Arpit Joshua Elias** | General AI Fluency, Week 4

## Workflow or agent

The distinction is not whether a model exercises judgment. It is who controls the sequence.

In a workflow, the steps are written down before anything runs. The model does the thinking inside each step, but a developer decided what the steps are, what order they come in, and when the process stops. In an agent, the model directs its own control flow: it decides what to do next, which tool to reach for, and when the work is finished, looping until it judges the task complete.

That framing matters because "agent" is used loosely enough to mean almost anything with an LLM in it. The useful test is: if I removed the model, would there still be a defined sequence? If yes, it is a workflow with a model inside it.

## My FL-04 pipeline is a workflow

My job application pipeline runs five steps: source, screen, select, tailor, then gate and compile. Every one of those is predetermined by me. The search terms live in a single file. The eight scoring dimensions are written into an operating manual. `verify_claims.py` runs on every CV because a rule says it must, not because the model decided a check was warranted this time. I state how many roles I want and it returns that many.

The model does make real decisions inside step 3. It reads job descriptions, weighs fit against missing requirements, and assesses interview risk. But judgment inside a fixed step is not the same as choosing the step. If I deleted the model tomorrow the sequence would still exist; it would just produce worse selections.

Two details settle it. My manual sets daily caps, so the system cannot decide today deserves ten applications. And rule 3 says a human submits, so the loop terminates at a person by design rather than when the model considers itself done.

That is not a shortcoming. The failure mode I built the system to prevent is overclaiming on a CV, and for that, predictable beats adaptive. An agent that decided for itself when honesty checks were warranted would be worse at the one thing the system exists to do.

## What MCP is

MCP, the Model Context Protocol, is a standard way for a model to reach things outside its own context. Rather than every tool inventing its own integration, a server exposes capabilities in a common shape and any MCP-speaking client can use them.

Three primitives:

- **Tools** are actions the model can invoke. Read a file, write a file, query a service.
- **Resources** are data the model can read. Files, records, documents.
- **Prompts** are reusable templates a server offers.

The important thing MCP does *not* do is change control flow. It grants capability. A workflow with a connector attached is still a workflow, because who decides the sequence has not changed. The model can now reach more, not choose more.

## What I connected, and what broke

I ran the official filesystem server against a copy of my job search workspace, connected to Claude Desktop, scoped to one directory.

Three tasks that plain chat could not have done:

**1. Listing the workspace.** It returned the eight folders and CLAUDE.md, reading from disk rather than from anything I had pasted.

**2. Reading the applications tracker.** It parsed 31 rows, found 6 with a date applied, and produced the status breakdown. It also caught something I had not: from row 21 onward the CSV is missing a delimiter, so every column shifts left. The CV filename lands in `applicant_count` and the real status lands in `cv_file`. It reconstructed the true statuses by scanning for keywords rather than trusting the column, and told me the underlying file needs fixing. That defect exists only in the file. No amount of chat could have surfaced it.

**3. Auditing the delivery folders.** It grouped every file by date folder, counted application packs, and identified that 2026-09-05 and 2026-09-06 tied at five each, 25 packs across the week.

Getting there was most of the work. `npx` was not on the PATH Claude Desktop could see, because Node was not installed at all. Once installed, the server still failed: my Windows username contains spaces, and the command was passed through `cmd.exe` unquoted, so it broke at `C:\Users\Arpit`. The fix was to invoke `node.exe` directly with the server script as an argument, since arguments get quoted properly and only the command does not.

One thing worth naming. The first working run reached a folder I had not intended to expose, because both my real workspace and the demo copy sat under the same parent. I moved the copy to an isolated path and deleted the original from that location. A filesystem server can write and delete, not only read, so scoping it deliberately is not a formality.

## One concrete agent upgrade

**Let it close the rejection loop.**

Right now my tracker records four rejections with reasons: high applicant volume, others more closely matched, no reason given. That information sits there and changes nothing. The next run screens exactly as the last one did, because the scoring dimensions are fixed in a file I wrote before any rejections existed.

The agent version would read the outcome history at the start of each run and decide what to do differently. If roles asking for three or more years keep rejecting at the application stage, it should weight that gap more heavily rather than waiting for me to notice and edit `job_filters.py`. If a role family produces responses, it should pursue more of them. It would also decide the day's volume from what the pool actually contains, rather than producing five because I asked for five.

That is a genuine shift in control flow. Today I decide the criteria and the count. There, the model decides both, based on evidence it gathers itself, and the loop terminates when it judges the day's queue good enough rather than when a number is met.

The honesty gate would stay exactly where it is. Adapting *what to pursue* based on outcomes is a reasonable thing to hand over. Adapting *what I am allowed to claim about myself* is not, and that boundary should hold no matter how agentic the rest becomes.
