---
title: "Pi Zero"
date: 2021-02-13T20:57:29Z
slug: ""
description: ""
keywords: []
draft: false
tags: [fun setups]
math: false
toc: false
---

*Updated Feb 22: details and clarification*

So last week I bought a Pi Zero hoping it could replace the AWS EC2 instance that I currently use as a SSH server for my iPad Pro. I use this to do actual programming work on the iPad, and overall, I'm pretty happy with this setup even though it's got a few warts.

My motivation for going with a local SSH server is mostly in not being dependent on a decent internet connection, though  price, control and ping are upsides as well. Going local is viable thanks to [Ethernet over USB](https://marcelwiget.blog/2018/12/02/tether-rpi-to-ipad-pro-via-ethernet-over-usb-c/)
in the first place: you can tether devices like a Raspberry Pi to an iPad *and* power them with a single cable. I think the idea was popularized by [this video](https://youtu.be/IR6sDcKo3V8).



I chose a Pi Zero specifically because it's inexpensive, uses [little power](https://www.jeffgeerling.com/blogs/jeff-geerling/raspberry-pi-zero-power) and should still be fast enough for my usecase. Further, the Magic Keyboard is full of magnets. Note all the little black squares in this xray:

![img](https://valkyrie.cdn.ifixit.com/media/2020/05/07123026/MagicKeyboard_X_watermarked-scaled.jpg)

(Source: [iFixit](https://ifixit.com/News/41291/dang-the-ipad-pro-magic-keyboard-looks-cool-in-x-rays))

Each of these is a tiny magnet, so I hoped that a Pi Zero would be small and light enough that it could be attached magnetically to the back of the Magic Keyboard while powering and connecting to it with a short angled cable, which would be pretty neat.

So I bought a bunch of neodymium magnets off AliExpress for like $2, and using the xray as a guide, I looked for a suitable position for a pair of magnets. Then I just glued them to a [Pibow](https://shop.pimoroni.com/products/pibow-zero-w) case with standard household glue after sanding them down a bit.

![img](../glue.jpg)

Surprisingly, the glue actually held up, and since the magnets are shaped like thin discs you can just stack as many as you need. In my case, four individual magnets stack up to be about as high as the screws on the Pibow:

![img](../height.jpg)

This way, the Pi is sitting flush against the back of the Magic Keyboard and doesn't wiggle. Here's the final result:

![img](../placed.jpg)

This is looking pretty sweet! Thanks to the magnets, it's easy to take it off or put it back on, though you should shut it down before disconnecting. USB over Ethernet works without hassle, and it doesn't kill battery life too much - I would guess you can get about 6-10h of active usage on the 11" iPad Pro, depending on workload. You can optimize it a bit by disabling the LED:

```bash
echo 0 | sudo tee /sys/class/leds/led0/brightness
```

Generally speaking, it does hit battery life noticeably, but it's not too bad - I can still get through a day with a single charge, and the Magic Keyboard lets you charge while using anyway.

So from a physical standpoint, it actually turned out that magnetically attaching the Pi works as well as it sounds in theory. However, there were other issues. 

For example, a short, angled cable is key - a convenient place to put the Zero is worth nothing if you have to deal with 2 meters of cable. And frankly, finding such a cable is a huge pain in the ass. I had to try several and ran into weirdness such as the orientation of the USB-C connector actually mattering for one cable, or another that would only deliver power from Micro USB to USB-C and not the other way around. In the end, [this one](https://www.amazon.de/-/en/Duttek-Adapter-MacBook-Android-Devices-black/dp/B078163B16/) worked for me.

Once I finally got things working, I started writing this blog post on the Zero as an initial experiment. This kind of boils down to just editing text files, but I'm using [Hugo](https://gohugo.io) which has a neat live preview server, and I wanted to get that running directly on the Pi Zero.

This is where I started running into software issues. The Hugo version in the official Raspbian repos is so old it wouldn't work with my theme. Not a problem, I thought, thankfully there's a recent version available in the Debian backports repo. 

Actually it was a problem though. The Pi Zero's BCM2835 is an ARMv6 CPU, a spec from **2002**! Coincidentally this is the exact same core used in the original iPhone, so it's kinda cool having this thing sit right on top of an A12Z. But the arch has its limitations - for example, it doesn't even have a [hardware divider](https://blog.regehr.org/archives/793). So running the Hugo binary from the backports repo merely yields:

```bash
$ hugo
[1]    6448 illegal hardware instruction  hugo
```

To get around this, I tried building Hugo from source, but ran into basically the same problem. It went and collected about 600 dependencies until it realized some of them required a more recent version of Go than is available in the Raspbian repos.

It took like 20 minutes just to get to that point, so I was not about to try also building Go from source on a Pi Zero. Luckily cross compilation is a thing, and [it's easy](https://www.thepolyglotdeveloper.com/2017/04/cross-compiling-golang-applications-raspberry-pi/) - I just ran this on my desktop:

```bash
git clone https://github.com/gohugoio/hugo.git
cd hugo
env GOOS=linux GOARCH=arm GOARM=6 go build
```

And after about a minute it had produced a binary that actually worked on the Pi Zero!

So luckily there weren't any unsolvable issues, and with this one out of the way, the Zero did the job just fine. It does work at a *very* leisurely pace, but my usecase doesn't need much power anyway. And honestly I kind of like that it takes its time. It's not so slow as to be unresponsive, and waiting a few seconds for it to build your site has got some relaxing quality to it.

However, one of the most annoying things about a VPS is moving files between it and the iPad, and I haven't really solved that on the Pi Zero yet. Currently I'm running a [Samba](https://www.samba.org) server on the Pi Zero, which is a lot more convenient than Blink's `scp` for example, though there are some quirks and it still takes a lot of clicks to copy a file over. So this is a bit suboptimal.

Interestingly there seems to be a way to [AirDrop files onto a Pi](https://owlink.org/2019/05/16/howto-use-airdrop-on-raspberry-pi-3.html) but it looks like this would prevent you from connecting the Pi to the internet using Wi-Fi. I might look into whether that can be solved at a later point. If I can get it to work, it'd be a perfect solution for this problem.

## Conclusion

Pro:

* One less subscription
* Not dependent on a decent internet connection
* No ping
* Full control
* Inexpensive
* Much more storage than cheap VPS usually offer

Con:

* Slow
* Have to plug/unplug it and boot/shutdown
* Draws extra power
* Extra dongle to carry around
	* (but it's literally a *computer* dongle which is pretty cool)
* Outdated repos
* It's still a workaround.

Overall I'll call this a win since most of the cons aren't that big to me personally. You might be wondering why I go through all this when I could just use a laptop, the answer is that I need a drawing tablet and I mostly [work on a desktop](../setups/), 
so if I can make my drawing tablet do the occasional desktop task, I'll prefer that over yet another device, even if it means putting up with some inconveniences. Finally, I just like the 11" form factor, and there's simply no 11" laptop to match the build quality and power of the iPad Pro.

As a final note, the [Banana Pi M2 Zero](http://wiki.banana-pi.org/Banana_Pi_BPI-M2_ZERO) 
might be an interesting Pi Zero alternative to improve the performance and software issues. It's the exact same form factor, and it packs four Cortex-A7 cores - that's ARMv7, so we [might](https://en.wikipedia.org/wiki/ARM_architecture#Arithmetic_instructions) 
get an actual divider among other things, plus it's in 40nm instead of the Pi Zero's 65nm so one can hope power efficiency is not too bad either. I will have to try this at some point to find out for sure.

