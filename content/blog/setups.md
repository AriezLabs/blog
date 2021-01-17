---
title: "The elusive perfect setup"
date: 2021-01-16T01:01:32+01:00
slug: ""
description: ""
keywords: []
draft: true
tags: []
math: false
toc: false
---

In the last few years, I have spent a lot of effort trying to find a nice computing setup. I've finally converged on something that I am pretty content with, at least right now during COVID and WFH. Of course, everybody has different needs, as a CS student I personally need a system that lets me take (preferably digital) handwritten notes and write code. With COVID, I also went back to playing video games more. So right now, my personal requirements are:

* Touchscreen and stylus
* Big screen for coding and lectures
* Something to game on

## 2017

In 2017, I started college with a 12" MacBook and 1st gen iPad Pro. This setup was pretty great. I couldn't really game, but back then you could have a social life, so that was fine. 

I *loved* the MacBook, it's a very convenient form factor, you could easily take it literally everywhere, it had USB-C docking, and it was just a pleasure to use in general. I think the original iPad Pro was a bit ahead of its time though, as in the tech wasn't quite ready yet. It got pretty warm when taking notes and I burned through almost half a charge in 3 hours of lectures. Back then my note taking system wasn't particularly sophisticated either (I was basically just taking standard handwritten notes in OneNote) and so I suspect I would've been just as happy with a pen and paper in place of the iPad.


## 2019

In 2019, the MacBook slowly started to show its age (it got a bit slower with each OS update, as always). So I moved on to a pretty beefy ThinkPad X390 Yoga, hoping that it could replace both my laptop and my tablet. 

Turns out, this kind of convertible is pretty awkward if you're typing something up and want to add a quick drawing. You either draw onto the erected screen (awkward) or you drop the screen to 180 degrees and draw (awkward) or you flip it (awkward). It's always *either* a laptop *or* a tablet, never both at the same time. And boy, is it a clunky tablet, both physically and from a usability standpoint. Neither Linux nor Windows are particularly usable with just a touchscreen, as is evident from (lack of) autorotate, tiny buttons, and many other minor annoyances that sum up into an unpleasurable experience.

The other issue with the X390 was shitty Linux support. The WiFi driver consistently crashed every couple of minutes when a Thunderbolt display was connected. Each crash froze the system for a few seconds and they occured once every few minutes, depending on kernel and driver version. It was really really annoying and I tried *everything* including submitting a kernel bug. No avail.

So while I had the highest expectations for this setup, I have to rate it the worst out of all I've had so far. Complete fucking disappointment, to be frank. The awkwardness of the form factor even would've been tolerable if the software wasn't close to unusable.


## 2020

When the lockdowns hit and I got bored, I dusted off my old gaming rig and turned it into a Hackintosh. This just took an afternoon of setup and it has been *rock solid* and probably my favorite computing device so far. Desktop upgradeability is worth a lot (I just recently upgraded to a 1TB SSD, paying roughly 17% of what Apple is charging) and you're not stuck with ultrabook thermals. For gaming, I kept it as a Windows dual-boot for a while, but later added a Fenvi PCIe WiFi card and replaced my useless nVidia GPU (no macOS drivers) with an AMD card. And so the need to dualboot was gone, as I can play LoL on macOS, and anything else on my [upgraded Xbox](../xbox/) with Game Pass.

In 2020 I also added an iPad Pro with the Magic Keyboard to the family. That thing has been the best implementation of the Convertible idea that I've seen so far. Thanks to the magnets it's a breeze to attach or detach the keyboard, so it's easy to type and add drawings. It also integrates seamlessly with macOS. I can take screenshots on my Hackintosh and mark them up on iPad, or AirDrop sketches directly to my Hackintosh. This is invaluable for my current note-taking system.

But still the iPad's nowhere near its potential. It's *seriously* limited by iPadOS. Basically, iPadOS is great for any everyday tasks, but as soon as you stray off the usecases that Apple has envisioned for you, you're fighting the OS.

Usually there is *some* workaround to achieve whatever you need, but compared to doing the same on a desktop OS these workarounds are usually ridiculously involved. [Blink](https://blink.sh/) is a livesaver in that it gives you a shell to work with, but it's remote and occasionally you do feel that.

But my gaming rig is getting old. It's a Skylake, SATA SSD, DDR3 RAM, all that jazz. Individually each of those doesn't have a massive impact on performance, but I imagine that a new rig overall could perform a lot better. However I'm not sure that that's worth dropping ~a grand on. The rig is still within *usable* realms. And I'm not sure how long Intel Macs are getting support from both Apple and other software vendors. I guess it'd be long enough that a new rig won't get dropped before it's quite slow anyhow. But again I don't really have a reason to go for a big upgrade right now. Intel's new Rocket Lake might be worth something, even though it's still 14nm, but since Apple is apparently not going to release new Intel Macs (for now), it'll be interesting to see whether they are supported well enough to be used as a daily driver. I would be going for a SFF build because they're sexy and I'm traveling a lot. 

The thing is I *want* to upgrade it but I literally can't justify it. Intel has stagnated so hard.

In any case, my current setup is the happiest I've been so far. The 12" MacBook was nice too, but it's just too slow for my needs right now. The iPad Pro is severely limited by software and you're locked in to Apple (maybe Asahi Linux can run on it someday? that'd be pretty amazing) but working on a VPS is still the least awkward compromise available right now. It's also well made in ways the X390 just wasn't (120hz, magnetic pen, actually usable as a <500g tablet unlike giant 13", 1.3kg hunk of metal).

## 2021

Due to the limitations imposed by iPadOS, I'm expecting to have to replace my desktop with a notebook at some point, though I want to see whether I can make the iPad work as my only mobile computing device first.

