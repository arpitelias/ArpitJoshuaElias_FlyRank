# Week 4: Choosing the Stack

**Arpit Joshua Elias** | General AI Fluency, Week 4

## My four constraints

**Free only.** No card, no trial that expires mid-build, no per-seat pricing.

**Honest skill level.** I can read and edit HTML and CSS but I have not built a site before. I am comfortable in Python and SQL, comfortable with Git and GitHub since all my internship work lives there. I have no JavaScript framework experience.

**What the portfolio needs to do.** Four pages: Home, Work, About, Contact. About sits off to the side as a detour. Two case studies on the Work page, strongest first. One action on every page, Book 15 minutes, wired to a Cal.com link.

**How the work must be displayed.** This is the constraint that decided it. My work is screenshots of executed notebooks, cropped output showing real numbers, plus links to a public GitHub repo. I need legible images at a sensible width and I need the repo link to be prominent. No image galleries, no embedded demo, no long-form reading beyond the case studies themselves.

**Does anything need to be dynamic?** Not yet, and probably not ever. Four static pages, a booking widget I do not host, and a repo link. Nothing needs a database, a login, or a server. I would rather say this plainly than build a backend I would then have to justify.

## Three options

### 1. Hand-written HTML on GitHub Pages (simplest)

**How I would build it:** four HTML files, one shared stylesheet, written by hand.
**Where it hosts:** GitHub Pages, free, from a repo named `arpitelias.github.io` which gives a clean root URL.
**Backend:** none.
**Trade-off:** every page repeats its own header and footer, so a change to the nav means editing four files. That is annoying at forty pages and irrelevant at four. No build step means nothing to break, but also no templating and no component reuse if the site ever grows.

### 2. A static site generator, Eleventy or Hugo (middle)

**How I would build it:** Markdown for the content, one layout template, a config file.
**Where it hosts:** Netlify or Cloudflare Pages, both free, or GitHub Pages with a build action.
**Backend:** none.
**Trade-off:** templating solves the repeated-header problem and case studies become Markdown files, which suits me since I have written everything in Markdown for eight weeks. The cost is a build step, a dependency tree and a new set of conventions to learn. If the build breaks the site does not deploy, and debugging a build I do not understand is exactly the kind of time sink that stops a portfolio getting finished.

### 3. Next.js on Vercel (most powerful)

**How I would build it:** React components, file-based routing, deployed from GitHub.
**Where it hosts:** Vercel free tier.
**Backend:** available if I want it, API routes included.
**Trade-off:** everything I might ever need, none of which I need. I have no React experience, so I would be learning a framework while trying to write case studies, and the framework would win. It also gives me capabilities that would tempt me into building features instead of finishing the site.

## Pressure-testing the front-runner

**What breaks if I pick the simplest?** Repeated markup across four files. At four pages this costs me a few minutes per nav change. It becomes a real problem somewhere around fifteen pages, and my sitemap says four, deliberately.

**What do I maintain if I pick the most powerful?** Node dependencies, framework upgrades, and a build that can fail for reasons unrelated to anything I wrote. I would be maintaining infrastructure rather than a portfolio.

**Can I finish in two weeks?** With option 1, yes, and I have already proved it: the site is live at https://arpitelias.github.io. With option 3 I would still be reading documentation.

**Does it show my work the way it needs to be shown?** Yes. My case studies are prose with cropped screenshots and a repo link. Plain HTML with a stylesheet does that as well as anything more complicated would, and my identity kit already specifies four hex codes and two Google Fonts, all of which drop straight into a stylesheet.

## Decision

**I chose option 1, hand-written HTML on GitHub Pages.**

The deciding constraint was how my work is displayed. If I needed image galleries or an interactive demo, options 2 or 3 would start earning their complexity. I need legible screenshots and a repo link, and plain HTML does that with nothing in the way.

I did not choose Eleventy because the problem it solves, repeated templates, does not exist at four pages. I would be paying a build step up front against a maintenance cost I may never incur. I did not choose Next.js because I have no React experience and learning a framework mid-build is how portfolios stay unfinished.

**Can I maintain this?** Yes, and that is not a guess. I have been committing to GitHub daily for eight weeks and I can read the HTML I wrote. If something looks wrong I can find it, because there is nothing between the file and the page. That is not true of a framework I do not know.

**Does it show my work well?** It will. The site is live and already carries my claim, my identity kit and my one action. Next week is filling pages that exist rather than starting from zero.

**The honest limit.** If the portfolio ever needs a blog, a filterable project list, or more than about a dozen pages, this choice stops making sense and I would move to option 2. I am choosing for the site I am actually building, not the one I might build later.
