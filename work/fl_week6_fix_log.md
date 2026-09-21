# Open It on Your Phone: fix log

**Arpit Joshua Elias** | General AI Fluency, Week 6
**Site:** https://arpitelias.github.io
**Checked on:** a real iPhone, plus laptop at desktop width

## How I looked

I did two passes. First I read through the repository itself, file by file, to see what the page asked for that might not exist. Then I opened the live site on my phone and worked through it as a visitor would: first screen, reading, tapping every link, using the contact form, opening the CV.

The repository pass found more than the phone did. Two of the problems below are invisible on screen and only show up if you look at what the page requests.

## What was broken, and what I changed

**1. The favicon did not exist.**
The page asked for `favicon.png` on every visit, and the file was not in the repository. Every page load produced a failed request, and the browser tab showed a blank default icon. I had specified the icon in my Week 3 identity kit and never uploaded it.
*Fix:* uploaded `favicon.png`, and added an `apple-touch-icon.png` for when someone saves the site to their phone's home screen.

**2. Sharing the link showed nothing.**
There were no preview tags, so pasting the URL into LinkedIn or a message showed no title, description or image. That matters more than it sounds, because my own brief asks me to link this site from LinkedIn, and a bare URL there looks like nobody finished it.
*Fix:* added Open Graph tags and a 1200 by 630 preview image carrying the claim, in the site's own colours.

**3. On a phone, the first screen was mostly empty.**
The layout used the same 5rem of space above the headline on every screen size. On a laptop that reads as calm. On a phone, with the browser's own bar on top, it pushed the headline down, and the headline then wrapped across three large lines. A visitor saw the claim and very little else before scrolling.
*Fix:* below 480 pixels wide, top padding drops to 2.5rem, the headline shrinks from 2rem to 1.6rem, and the gaps between sections tighten. The headline now fits on two lines and the case study starts on the first screen. Desktop is unchanged.

**4. Footer links were small targets.**
The four footer links sat in a row at small text size, close enough together that a thumb could catch the wrong one.
*Fix:* every footer link and button is now at least 44 pixels tall with more space between them.

## What I checked and found fine

- **Body text:** 16 pixels, readable without zooming. Contrast was already verified in Week 3: body text 16.65:1, accent 6.91:1, both pass.
- **Contact form:** fields are 16 pixel text, which stops iPhones zooming in awkwardly when you tap into them. The test submission from Week 6 still arrives.
- **Every link:** LinkedIn, GitHub, CV, and both booking buttons all open the right place.
- **CV:** opened on the phone. It is the full document, despite being a small file at 5.7 KB.

## What I did not fix, and why

**There are no work images on the site.** The criteria check that work images are crisp, and mine are absent rather than blurry. The case study describes a job where there is nothing I can publicly screenshot, so the honest choice is prose. My Week 3 content map planned a second case study built from my FlyRank notebooks, which would carry real captures, and that is the natural place to add images rather than inventing something decorative for this one.

## Before and after

Phone screenshots attached to the submission. The before shot was taken in an in-app browser and the after in the regular browser, so the browser chrome differs slightly, but the page itself is directly comparable: the gap above the headline and the three-line wrap are gone.
