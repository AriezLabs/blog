---
title: "Virtualization"
date: 2021-03-14T11:40:23+01:00
slug: ""
description: ""
keywords: []
draft: false
tags: [setups, fun, technical]
math: true
toc: false
---

This week I've played around with virtualization a bit. I wanna give a high level overview of the project first, and then dive into a few details.

I'm currently using a i7-6700, 16GB RAM, Radeon RX570 Hackintosh and the goal was running both a virtualized Windows *and* macOS on that machine simultaneously, using Linux as host. The RX570 would be passed through to the Windows VM for gaming, with macOS getting the iGPU as "work OS" and Linux just running headless. To switch OSes, I would just change my monitor's input device, and switch the mouse+kb over by connecting remotely to [`virt-manager`](https://virt-manager.org/) running on the host.

This was intended as kind of a feasibility study purely on the software side. My system's specs are probably a bit too limited to practically run three OSes simultaneously, so I was thinking if this test run yielded satisfactory results (modulo performance), I'll consider finally upgrading my system.

I even did get it to work in the end. *Mostly*. It took a lot of experimentation to get everything running, but in the end I was able to fix any issues except unusable audio on macOS. This seems to be a [widespread issue](https://www.google.com/search?q=macos+kvm+choppy+audio), and a fix may turn up yet, so I'll update this post if it ends up working after all. But right now it's kind of a dealbreaker.

And there's another big thing taking the wind out of this project's sails: it's just not that useful for me. The hassle involved in switching VMs is only marginally smaller than what a dualboot would take. This might be different with a second monitor and/or a [KVM switch](https://en.wikipedia.org/wiki/KVM_switch), both of which I will be able to test out next weekend, so we'll see about that. If I can get audio and hassle free switching I'll consider it worth it. But otherwise I'll just stick with my bare metal Hackintosh install.

With all that said, it's pretty amazing tech and it works extremely well for what it is. If it fits your usecase better than mine it's probably worth it - for example, if you need Windows for more than just the occasional gaming session, or if you don't need macOS, in which case you'll save yourself quite the PITA since it's pretty much a hostile guest OS.


## Setup

For the host, I used Arch btw, but kept it pretty minimal since I'm not planning to do much on it. I set up a macOS VM using [this Git repo](https://github.com/kholia/OSX-KVM). This is one of two major git repos taking most of the work out of setting up a macOS VM (the other being [this](https://github.com/foxlet/macOS-Simple-KVM)) and it's got a lot of useful guides but the documentation is a bit sparse. I found the best way to use it is to just grep it for whatever you're looking for. 

In general, you just have to download macOS, create a virtual hard disk, and point QEMU at it. The repo comes with a preinstalled and -configured OpenCore bootloader image. You can then boot the VM and install macOS normally.

At least in theory. I ended up constantly getting [PKDownloadError 8](https://apple.stackexchange.com/questions/372785/pkdownloaderror-error-8-upon-catalina-update) during install. This was related to DNS settings - using OpenDNS on the host and then using a tap device for guest networking solved it. It still took several tries to install though - the error seemed to happen somewhat randomly, and I had to restart the installation a couple times until it went through. 

There were no further issues once the install completed, and so I went ahead and tried to get PCI passthrough working. The Arch wiki has a pretty helpful [article](https://wiki.archlinux.org/index.php/PCI_passthrough_via_OVMF) on that. Initially I tried to pass the iGPU through to macOS using the QEMU CLI, but I couldn't get that to work, so I decided to pass the dGPU to Windows using `virt-manager` instead, hoping that would be easier.

And it turned out that it was - mostly I just had to follow the wiki guide, but I did run into one issue: since I was passing through the dGPU, I had to boot Arch off iGPU, but my mainboard seems to ignore the setting for the primary graphics device. It would just always boot off the dGPU, and then of course the `vfio` driver took over and I'd just get no output at all. So I only connected the dGPU to the display once I booted the Windows guest.

Finally, after booting, I got like half a minute of blackscreen, then the Windows login screen popped up in a solid 800x600 resolution! Never before had I been so happy to see something this ugly. 

I installed the drivers and went ahead and did some experiments.


## Performance

Testing League of Legends on Windows 10, I was actually getting *twice* the FPS that I'm getting on bare metal macOS. So that was quite a surprise, and I'm not sure whether to blame Riot or Apple, but League isn't really a demanding title anyway. To get a better idea of the performance, I also tested Fallout 4, which ran smoothly without issues save for occasional stutters that I didn't get in League. They occured seldom enough to not be annoying though. 

Sadly I don't have a bare metal Windows install to compare actual framerates against, but subjectively, the VM delivered completely sufficient gaming performance. I was actually pretty amazed by experiencing low input lag, high FPS, high resolution and non-shitty input devices again, having played video games mostly on an OG Xbox One for the past year or so. I was actually missing out.


## macOS

So with the Windows side of things working, and with some more experience under my belt, I went on and managed to pass the dGPU through to macOS as well. Using `virt-manager` for the macOS VM as well now, it pretty much Just Worked$^\text{TM}$. But before I got around to passing through the iGPU I noticed the aforementioned audio issues, and those are a higher priority fix - why set up iGPU passthrough when I can't even listen to music yet?

I've got some digging to do - I'm just hoping this issue is fixable, because both audio devices I tested this with have an USB interface. I'm not sure whether HDMI or onboard audio work, but I don't think it's a good sign that not even USB soundcards are working. So far I've only tried using a different audio kext, so there's hope, but if nothing else helps, I'll probably try going back to Catalina and see if I can get that to work.

Update/conclusion coming once I get things working!

