# Make It Do Something: a working contact form

**Arpit Joshua Elias** | General AI Fluency, Week 6
**Live on:** https://arpitelias.github.io, under "Not ready for a call?"

## Why this feature

My site already had a booking link. But the person I am writing for, a data governance lead at a pharma company, often cannot book a call as a first move. They may need to forward me to a colleague, check something internally, or just want to ask a question first. With only a booking link, that person had nowhere to go. A short form that lands in my inbox covers them.

One feature, not several. I did not add a newsletter, comments or anything else.

## What a backend is

A website has two halves. The front end is what you see: the text, the layout, the button. The backend is whatever sits behind it and does something when you press the button: stores the data, sends the email, runs the calculation.

My site has no backend of its own. GitHub Pages only hands out files. If someone sends it information, it has nowhere to put it and nothing to do with it. That is fine for reading a page and useless for a form.

So I borrowed one. Formspree is a free service whose whole job is to be the backend for a form. It receives the submission and turns it into an email.

## How the data flows

1. A visitor fills in their name, email and message on my page.
2. When they press Send, the browser does not send it to GitHub at all. The form's address points at Formspree, so the browser packages the three fields and posts them straight there.
3. Formspree checks it. There is a hidden field on the form that people never see but bots fill in automatically, because bots fill in every field they find. If that hidden field has anything in it, Formspree treats the submission as spam and drops it.
4. If it passes, Formspree emails it to me, using the subject line the form told it to use, so these do not get lost in my inbox.
5. The visitor sees a confirmation page from Formspree.

The part I found most useful to understand: my site never touches the message. It goes from the visitor's browser to Formspree to my inbox. GitHub only served the page the form sits on.

## The test

I opened the site in a private window, filled the form in from a second email account, and sent it. The first submission to a new form made Formspree ask me to confirm the form by email, which is its way of stopping someone using my form to spam me. After that, the submission arrived: name, email and message all intact, subject "Portfolio contact form".

One thing I noticed. The email says it was submitted at 12:25 PM, but it reached me at 1:25 PM by my clock. Formspree records time in UTC, and Ireland is an hour ahead in September. Nothing was wrong, but it is the kind of thing that would matter if I ever needed to prove exactly when someone got in touch.

## Limits

It is on a free tier with a monthly submission cap. The confirmation page is Formspree's, not mine. And the message lives in my inbox, not on my site, so if I lost that email I would have no other copy. For a portfolio that is the right trade: nothing to host, nothing to maintain, and one thing that genuinely works.
