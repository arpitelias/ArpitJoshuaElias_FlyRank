# DNS, explained so a non-technical colleague could follow it

**Arpit Joshua Elias** | General AI Fluency
**Site:** https://arpitelias.github.io

## The problem DNS solves

Computers on the internet find each other by number, not by name. Every machine that answers web requests has an address like 185.199.108.153. Nobody wants to remember that, and the number can change without the website changing, so we use names instead.

DNS, the Domain Name System, is the service that turns a name into the current number. It is closer to a phone directory than a switchboard: it tells you where to call, it does not carry the call.

## What actually happens when someone types my address

Say a colleague types `arpitelias.github.io` into their browser.

**1. The browser checks what it already knows.** It keeps recent answers for a short while. If it looked this up two minutes ago it will reuse that and skip everything below. Your operating system keeps a similar short-term note.

**2. It asks a resolver.** If nothing is cached, the browser hands the name to a resolver, usually run by your internet provider, sometimes one you have chosen like Cloudflare's. The resolver's job is to do the legwork and come back with a number.

**3. The resolver works right to left.** Names are read backwards, from the most general part to the most specific. So it starts at the top of the tree and asks who is responsible for `.io`, then asks that server who is responsible for `github.io`, then asks that server about `arpitelias.github.io`. Each answer is a pointer to the next place to ask, not the final answer. Two or three hops, and they are fast.

**4. The nameserver that actually holds the record answers.** At the end of that chain sits the authoritative nameserver, the one holding the real records for the name. It sends back the record.

**5. Now the browser can connect.** It opens a connection to that number and asks for the page. Everything up to this point has been about finding the address. Nothing has been downloaded yet.

The part I had backwards when I first thought about this: I assumed the browser contacted the host and the host looked up the name. It is the other way round. The lookup finishes first, entirely outside the host, and nothing can be requested until the name has become a number.

## What a CNAME record is

The record types are just different kinds of entry in the directory.

An **A record** points a name straight at a number. `arpitelias.github.io` has A records pointing at GitHub's servers.

A **CNAME record** points a name at *another name* rather than a number. It means "this is an alias, go and look that one up instead". So if I bought `arpitjoshua.com` tomorrow and wanted it to serve my site, I would not point it at GitHub's numbers. I would add a CNAME saying `www.arpitjoshua.com` is an alias for `arpitelias.github.io`, and the resolver would follow it.

**Why the alias is better than the number.** If GitHub changes the servers behind `arpitelias.github.io`, they update their own records and my alias keeps working. If I had written GitHub's numbers into my own records, the day they changed, my site would go dark and I would have no idea why. Point at the name and let whoever owns that name keep it current.

## Why changes are not instant

Every record carries a TTL, a time to live: how long anyone is allowed to keep the answer before asking again. If the TTL is an hour, a resolver that looked up your name five minutes ago will keep serving the old answer for another fifty-five minutes, even after you have changed it.

This is why a DNS change can look broken. Your machine sees the new site, a colleague sees the old one, and neither of you is wrong. You are reading cached answers of different ages. The usual advice to "wait a bit" is really "wait for the caches to expire".

## Where my site sits in all this

I have not bought a domain. `arpitelias.github.io` works because of a naming convention: name a GitHub repository after your username followed by `github.io`, and GitHub serves it at that address. GitHub owns `github.io` and holds the records for everything under it, so I am using their name rather than one of my own.

The certificate that makes the padlock appear is separate from DNS but depends on it. GitHub can prove it controls that name, so it can obtain a certificate for it, which is why HTTPS works on a site I did not configure.

If I connect my own domain later, the only thing that changes is step 4: a different nameserver holds the record, and that record points back here by alias. The rest of the chain is identical.
