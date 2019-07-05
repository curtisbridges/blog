---
title: "Trash files from the command line"
categories:
  - commandline
  - homebrew
tags:
  - shell
  - homebrew
---

I often use the `rm` and `rmdir` commands from the command line as any normal shell user does.
However, there are times when I want to move files to the macOS trash, just in case I need to
restore them for whatever reason. I wondered -- is there a utility for this?

Of course there is.

After a quick Google, I found this: [https://hasseg.org/trash/](https://hasseg.org/trash/). As
the page suggests, you can install via Homebrew:

```
brew install trash
```

Once installed, you can easily invoke it via:

```
trash foo.txt
```

Granted, it isn't going to be a widely used command, but something I wanted to use in a few
specific cases.
