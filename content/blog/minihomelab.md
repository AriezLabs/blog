---
title: "Minihomelab"
date: 2021-01-26T15:11:50+01:00
slug: ""
description: ""
keywords: []
draft: true
tags: []
math: false
toc: false
---

* Setup archivebox, pretty easy just follow their tutorial
  * https://github.com/ArchiveBox/ArchiveBox
  * Lots of random errors but in the end things work fine enough
* Set a short hostname so now I can reach the thing at `mini.local`

```sh
# install the archivebox package using homebrew
brew install archivebox/archivebox/archivebox

# create a new empty directory and initalize your collection (can be anywhere)
mkdir ~/archivebox && cd ~/archivebox
npm install --prefix . 'git+https://github.com/ArchiveBox/ArchiveBox.git'
archivebox init
archivebox --version

# start the webserver and open the web UI (optional)
archivebox manage createsuperuser
archivebox server 0.0.0.0:8000
open http://127.0.0.1:8000

# you can also add URLs and manage the archive via the CLI and filesystem:
archivebox add 'https://example.com'
archivebox status
archivebox list --html --with-headers > index.html
archivebox list --json --with-headers > index.json
archivebox help  # to see more options
```

Also installed mopidy which works *meh*

## Todo

Now to make it reachable from the web.

* Your router probably needs a static external IP?
* Not sure if mine's got one
* If it's got one, I can point my DNS at some port in my router, and forward that port to the Mini
* I got a LTE router and generally the connection sucks but LTE comes with nice uplink
* Otherwise there are dynamic DNS services such as
  * noip
  * https://freedns.afraid.org/
  * https://github.com/ddclient/ddclient
* Maybe I'll keep it all local for now.

Finally, projects to run.

* Mosh for Blink on iPad
  * it's probably going to suck due to poor connection compared to a VPS in a datacenter
  * but maybe not actually *that* bad
  * and at least if I'm home, it's instant
  * maybe I can set it up to create its own WiFi and so I'd just need to carry that thing with me...?
* Setup Xcode server?
* Install the second HDD and move ArchiveBox there and setup Time Machine Backupz
* Host Zettelkasten
* Probably *not* host my blog on there after all
  * it's not exactly a challenge nor would I learn much from doing it if I've already setup everything else I mentioned
  * Separated hosting for private and public stuff
  * The private server is still SPOF for all my private stuff, but it's lower profile due to the separation
  * Probably don't wanna use docker for safety without upgrading ram
* Look into security https://blog.prutser.net/2021/01/20/how-to-securely-self-host-a-website-or-web-app/
* Build a landing page with:
  * time
  * disk usage
  * ...

