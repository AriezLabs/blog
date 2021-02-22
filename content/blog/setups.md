---
title: "The elusive perfect setup"
date: 2021-01-17T23:46:32+01:00
slug: ""
description: ""
keywords: []
draft: false
tags: [setups]
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

In 2019, the MacBook slowly started to show its age (it got a bit slower with each OS update, as seems to be common with Apple). So I moved on to a pretty beefy ThinkPad X390 Yoga, hoping that it could replace both my laptop and my tablet. 

Turns out, this kind of convertible is pretty awkward if you're typing something up and want to add a quick drawing. You either draw onto the erected screen (awkward) or you drop the screen to 180 degrees and draw (awkward) or you flip it (awkward). It's always *either* a laptop *or* a tablet, never both at the same time. And boy, is it a clunky tablet, both physically and from a usability standpoint. Neither Linux nor Windows are particularly usable with just a touchscreen, as is evident from (lack of) autorotate, tiny buttons, and many other minor annoyances that sum up into an unpleasurable experience.

The other issue with the X390 was shitty Linux support. The WiFi driver consistently crashed every couple of minutes when a Thunderbolt display was connected. Each crash froze the system for a few seconds and they occured once every few minutes, depending on kernel and driver version. It was really really annoying and I tried *everything* including submitting a kernel bug to no avail.

So while I had the highest expectations for this setup, I'm rating it the worst out of all I've had so far. It was a complete disappointment, to be frank. The awkwardness of the form factor even would've been tolerable if the software wasn't close to unusable.


## 2020

When the lockdowns hit and I got bored, I dusted off my old gaming rig and turned it into a Hackintosh. This just took an afternoon of setup and it has been *rock solid* and probably my favorite computing device so far. Desktop upgradeability is worth a lot (I just recently upgraded to a 1TB SSD, paying roughly 17% of what Apple is charging) and you're not stuck with ultrabook thermals. For gaming, I kept Windows installed in parallel for a while, but later added a Fenvi PCIe WiFi card and replaced my useless nVidia GPU (no macOS drivers) with an AMD card. And so the need to dualboot was gone, as I can play LoL on macOS, and anything else on my [upgraded Xbox](../xbox/) with Game Pass.

In 2020 I also added an iPad Pro with the Magic Keyboard to the family. That thing has been the best implementation of the Convertible idea that I've seen so far. Thanks to the magnets it's a breeze to attach or detach the keyboard, so it's easy to type and add drawings. Hardware-wise, the CPU is so fast you are just not going to max it out, the 120Hz display is sweet, build quality is superb as always, plus it's very lightweight which means it's also a comfortable reading device. 

It also integrates seamlessly with macOS. I can take screenshots on my Hackintosh and mark them up on iPad, or AirDrop sketches directly to my Hackintosh. This is pretty invaluable for my current note-taking system.

But still the iPad's nowhere near its potential. It's *seriously* limited by iPadOS. Basically, iPadOS is great for any everyday tasks, but as soon as you stray off the usecases that Apple has envisioned for you, you're going to be fighting the OS. Usually there is *some* workaround to achieve whatever you need, but compared to doing the same on a desktop OS these workarounds are usually ridiculously involved. For example, to get an IDE, you can set up [code-server](https://github.com/cdr/code-server) on your VPS and add a bookmark to it on your home screen. [Blink](https://blink.sh/) is also a livesaver in that it gives you a proper shell to work with. But both Blink and code-server are remote and occasionally you do feel that.

There's an upshot to iPadOS's locked down mobile OS nature though: it's a perfectly usable tablet OS. (And this is not a given, as I've learned the hard way.) On iPadOS, things like autorotate just work, you get smooth logins via FaceID, there's generally no fiddling around with technical issues like your microphone not working on a Zoom call, and so on.

In general, I find that the pros outweigh the cons, especially since I can just use my Hackintosh for anything iPadOS doesn't want me to do, and so this is my favorite setup so far.


## 2021 and on

Due to the limitations imposed by iPadOS, I'm expecting to have to replace my desktop Hackintosh with a notebook once I'm on the go more often again, though I want to see whether I can make the iPad work as my only mobile computing device first. 

While Apple Silicon is looking like a gamechanger in the notebook market after years of Intel stagnation, I'm not particularly fond of being locked in to Apple, especially seeing the recent big tech censorship events, so I'm happy to see more open alternatives like the [X1 Nano](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-x1/ThinkPad-X1-Nano/p/22TP2X1X1N1) or [X12 Detachable](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-x/X12-Detachable-G1/p/22TPX12X2D1) pop up in the sub-kilogram and convertible markets respectively, as well as progress being made on the software side (see e.g. [JingOS](https://www.jingos.com/)).

