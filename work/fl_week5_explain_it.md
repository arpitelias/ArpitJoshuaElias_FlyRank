How a file I saved on GitHub ends up as a page on the internet

I put a file called index.html in a GitHub repository and a minute later the page was live at arpitelias.github.io. I did not know what happened in between, so I found out.

First surprise: a GitHub repository is not a web server. It stores my files and their history, and it has no idea what a web page is. So something else has to take those files and put them somewhere a browser can reach. When I switched Pages on, GitHub started running a small job every time I commit. That job takes a copy of my files and pushes them onto machines whose whole purpose is answering web requests. Turn Pages off and the file stays in the repo, perfectly safe, and the site goes dark.

Second surprise: the browser does not go to GitHub first. Computers on the internet find each other by number, not by name. So when someone types my address, the browser first asks the internet's directory service what number sits behind that name. Only once it has the number does it open a connection and ask for the page. I had these the wrong way round: I assumed the browser knocked on GitHub's door and GitHub looked up the name. It's the other way round, and nothing can happen until the name has been translated.

Third thing I did not expect: the copy answering that request usually is not in one place. It sits on machines spread around the world, and you get whichever one is nearest. That is why a page hosted for free loads quickly from Ireland.

The name works because of a naming rule rather than anything I bought. Name a repository after your username followed by github.io and that becomes your address.

What this changed: I was treating my site as one thing. It is really three. A place my files live with their history, a job that copies them out to be served, and a name that points at where they landed. Any of the three can break on its own.
