# Break Your Own Site

**Arpit Joshua Elias** | General AI Fluency, Week 7
**Site:** https://arpitelias.github.io

## How I tried to break it

Five deliberate attempts on the contact form, then a pass through the code for things clicking cannot reveal, then a speed check.

| Attempt | What happened |
|---|---|
| Submit the form completely empty | Nothing sent. The browser blocked it on the required fields. |
| `notanemail` in the email field | Browser refused and asked for a real address. |
| Send a real message, press back, send again | **Both went through.** Two identical messages in my inbox. |
| Paste several paragraphs into the message box | Sent fine. |
| Look at where I land after sending | **Formspree's page, not mine.** I had to press back to return. |

Also opened the site in a browser I had not used for it and clicked every link, including the CV, both booking buttons and the two case study images. All fine.

## Findings, triaged

### Fix-now

**1. After sending a message, the visitor was handed to a third party.** The weakest moment on the site was immediately after the one action I want people to take: a confirmation screen belonging to Formspree, with my name nowhere on it and no route back except the back button.
*Fixed:* built `thanks.html` in my own styling and told the form to return there. It confirms the message arrived, says when I reply, and still offers the booking link.

**2. The page title was only my name.** A search result would have said "Arpit Joshua Elias" and nothing about what I do.
*Fixed:* now reads "Arpit Joshua Elias | Data quality and governance, Ireland", with a canonical tag added.

**3. No robots.txt or sitemap.xml.** The two files a search engine looks for first were both missing.
*Fixed:* both added, with robots pointing at the sitemap.

**4. Fonts loaded from Google on every visit, and it was the single biggest thing slowing the page.** I decided in Week 5 to self-host them and never did. The speed check gave me the cost: render-blocking requests, estimated saving 2,370 ms on mobile.
*Fixed:* the three font files are now served from my own site, with their open font licences included. Mobile performance went **87 to 100**, desktop 99 to 100. Largest Contentful Paint 3.2s to 0.8s, Speed Index 3.2s to 0.8s. Render-blocking requests no longer appears in the report at all.

**5. No 404 page.** A mistyped address showed GitHub's default, which looks like the site is broken rather than the address being wrong.
*Fixed:* added a plain 404 page in my own styling that says nothing is broken and offers a way back.

### Known limitations, named not hidden

**Duplicate submissions still go through.** Pressing back and sending again delivers twice. I have left it: on a contact form the cost is a repeated email, and the fixes available on a static site are either client-side JavaScript that a determined refresh defeats anyway, or a backend I do not have. If this were taking payments it would be a fix-now.

**The form depends on a free third-party service with a monthly cap.** If Formspree is down or the cap is hit, messages are lost silently rather than bouncing. There is no second route except the email in my reply and the booking link.

**No message is stored on my side.** Submissions live only in my inbox. If I lost that email I would have no other copy.

**Nothing validates that the message is genuine.** The hidden honeypot field catches naive bots. A person typing nonsense gets through, and that is the right trade for a contact form.

**Remaining speed items are not worth fixing.** The report still lists cache lifetimes and image delivery, worth about 84 KiB and 10 KiB. Cache headers are not something I control on GitHub Pages, and the images are already small, cropped notebook captures. Performance is 100 on both mobile and desktop, so I would be optimising a number rather than an experience.

## Before and after

| | Before | After |
|---|---|---|
| Mobile performance | 87 | 100 |
| Desktop performance | 99 | 100 |
| Largest Contentful Paint (mobile) | 3.2 s | 0.8 s |
| Speed Index (mobile) | 3.2 s | 0.8 s |
| Render-blocking requests | 2,370 ms | not listed |
| Accessibility / Best Practices / SEO | 100 / 100 / 100 | 100 / 100 / 100 |

## What I took from it

The clicking found two real problems and the code reading found three, including the biggest one. The fonts had been slowing every visit for weeks, I had already decided to fix it, and nothing in the browsing experience told me. It took a measurement to make it visible, which is close enough to my own claim about data that I should have noticed sooner.
