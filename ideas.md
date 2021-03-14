* Virtualization setup
  * Testing with just quad core Skylake i7 and 16GB RAM, and a RX570
  * Takes a bunch of fiddling around but did get the passthru running
  * to both macOS and windows, use kholia/OSX-KVM repo
  * the idea was headless Arch, macOS on iGPU, Win10 on dGPU. Switching devices using virt-manager, n shit
  * win10 perf was sweet... FO4 running in 1440, some stutters but only occasionally and not too bad.
  * macOS: Audio not working properly.
    * Not sure what that was due to
    * even with usb audio devices...
    * maybe needs a PCI sound card... idk
  * Also, Hackintosh wouldn't boot unless VT-d is disabled in mobo
* Idk, notes on Mac Mini pt2/3...?
  * Installing extra HDD, and installing Jitsi Meet homework.
  * Your router probably needs a static external IP?
  * Not sure if mine's got one
  * If it's got one, I can point my DNS at some port in my router, and forward that port to the Mini
  * I got a LTE router and generally the connection sucks but LTE comes with nice uplink
  * Otherwise there are dynamic DNS services such as
    * noip
    * https://freedns.afraid.org/
    * https://github.com/ddclient/ddclient
  * Maybe I'll keep it all local for now.
  * Finally, projects to run.
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



* Taking notes, or: yet another Zettelkasten blog post
* Accounting? Motivation, LSA book review and some PTA system?
  * Motivation:
    * Be prepared for emergencies
    * Recognize unneccessary spending
    * Save money consistently
    * Not directly necessary for everyone, but worth it if your financial situation is complicated
* Misinformation and reasoning by principles
  * Example?
* The merits of video games
* Fallout 3 on iPad (couldn't get it to work)
* On focusing on fewer things
* Primer on growing medical MJ
* My current COVID routine
* App Devblog

