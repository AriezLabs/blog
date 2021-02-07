---
title: "Homelab pt.3"
date: 2021-02-07T17:49:11+01:00
slug: ""
description: ""
keywords: []
draft: false
tags: []
math: false
toc: false
---

I'm generifying the title of this series, because with the latest addition, the lab's not just a Mac Mini anymore. I've dusted off my Raspberry Pi, which I habitually do, roughly every couple of months, intending to start some project until interest wanes about two weeks later and the Pi goes back on the shelf. This time I've hooked it up to my TV and installed [RPiPlay](https://github.com/FD-/RPiPlay), and I've got a feeling that the Pi has finally found a good home.

RPiPlay is an AirPlay server for Raspberry Pi - it'll let you mirror your iPhone's screen to your TV, for example. This would otherwise require an Apple TV or a decent smart TV. If you're too broke for either or don't trust smart TVs, this is for you! (I tick both boxes 🙃)

Mirroring your iPhone to the TV might not seem that useful at first, but I think it actually offers the best user experience for watching Youtube on a TV. Everyone knows the pain of typing search queries with a TV remote, or clicking through some shitty playlist view where you can't see more than three videos at once. Somehow, TV UX is basically stuck in the era of pre-iPhone mobiles.

So by mirroring your iPhone, you skip all of that bullshit and get a smartphone UI which is far more usable. Plus, you can of course also put any other app on the big screen, so looking at photos or even browsing the internet on your TV is now easy.

And if you do it on a Pi, you can also have it do all the other smart TV duties, but without the spying. It can access a NAS and play movies easy. It can go on Youtube and Netflix. It can't do cable TV but who the hell wants that anyway?

There are still more gotchas: 

* Resolution is limited to that of your iPhone (unless you mirror your Mac or iPad)
* While RPiPlay does mostly just work, it's got some quirks:
  * The connection is occasionally flaky
  * Sometimes you can't exit it
  * To get working audio I had to run with `-l -a hdmi` switches
* There will be black bars
* You will want a trackpad+kb combo
* It's only AirPlay 1 which, most notably, has about a second of delay.

Ultimately though I think the superior UX wins out against all of that. Except for the connectivity and performance issues, none of them are really annoying, and I've got some improvements left to do that might improve these (using a wired connection for the Pi and rebuilding with `-O3`). So I'll see whether that does anything, and even if not, I basically got Apple TV functionality for free. And that's sweet. 

