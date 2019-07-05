---
title: "GitHub Access Behind Firewalls"
excerpt_separator: "<!--more-->"
categories: [devtool]
tags: [github, git, ssh, tools]
---
I had to get new tires and an oil change. I wanted to use the downtime to get some work done from the Dunkins' next door. I sat down, with my laptop, attempting to get some coding done from a chair in the corner. I attempted to pull down a repository from GitHub and saw:

```
ssh: connect to host github.com port 22: Connection timed out
```

After some Googling, I discovered this solution: [https://stackoverflow.com/a/52817036](https://stackoverflow.com/a/52817036)

In short, you can force git access to GitHub repos to an alternate server/port by editing your `~/.ssh/config` file:

```
Host github.com
 Hostname ssh.github.com
 Port 443
```

After that, I could easily `git pull` until my heart's content!
