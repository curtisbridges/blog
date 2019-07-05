---
title: "Running Jekyll using Docker"
excerpt_separator: "<!--more-->"
categories:
  - learning
  - blog
tags:
  - blog
  - devops
  - Docker
  - Jekyll
---

Ruby and I don't get along.

<!--more-->

I tried several methods to get a proper Jekyll install working on my dev computer. I'm not a ruby person; eventually, I could have figured it out. I wanted a better solution than having to learn enough of the ruby ecosystem and hoping that I would remember enough long-term to keep it stable on my system.

I tried using the macOS default ruby (which is a bit out of date, of course). I tried installing the latest via homebrew (and got close to a working solution) and I didn't even try installing `rbenv` or `rvm` since I only wanted a working jekyll.

Enter: Docker.

Docker allows you to use pre-canned images for all sorts of purposes. I was sure I could find an image that fit my use case -- I was sure it wasn't all that unique.

1. Install Docker using homebrew:
```
brew cask install docker
```
- Note: `brew install docker` lacks the docker daemon, which is usually provided by VirtualBox. See: [https://stackoverflow.com/a/40523608/6385823](https://stackoverflow.com/a/40523608/6385823)

We want a working Docker on our system and the easiest path to that is the [Docker Desktop for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac). As with all my installs, I prefer to use homebrew or homebrew casks when they are available.

2. Create a new jekyll site in current directory:
```
docker run --rm --volume="$PWD:/srv/jekyll" -it jekyll/jekyll jekyll new .
```

3. Install all jekyll dependencies in the Docker container:
```
docker run --rm --volume="$PWD:/srv/jekyll" -it jekyll/jekyll jekyll build
```

4. Run jekyll server as a Docker container:
```
docker run --name newblog --volume="$PWD:/srv/jekyll" -p 4000:4000 -it jekyll/jekyll jekyll serve --watch --drafts
```
The `--name` option can be any unique string; I chose `newblog` as the example used here.

5. Open your browser to [http://0.0.0.0:4000](http://0.0.0.0:4000)
Localhost will also work rather than the Docker specific 0.0.0.0.

6. Hot reload changes:
```
docker restart newblog
```
Since the jekyll container is launched with the `--watch` flag, it should update as content is modified. However, if there are configuration changes, you might have to restart the container.

7. Removing the container:
```
docker rm -f newblog
```

Most helpful site when trying to achieve this task: [https://ddewaele.github.io/running-jekyll-in-docker/](https://ddewaele.github.io/running-jekyll-in-docker/)
