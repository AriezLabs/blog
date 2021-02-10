* RPi Zero
  * cable didn't work, care: has to charge USB C *to* micro USB. data seems to be bidirectional
  * other cable works, but only if plugged in in a specific orientation
  * set up according to https://marcelwiget.blog/2018/12/02/tether-rpi-to-ipad-pro-via-ethernet-over-usb-c/
  * Stuck magnets to it
  * connected!
  * overll, seems to only pull a little more power than is typical
    * 0.4W idle
    * compiling Hugo took like 6% battery per hour
  * tried to run a hugo server on the PI and access it in Safari
  * first, had to `git submodule init`
  * then, hugo version in the repos was too old for my theme
  * then, tried buster-backports repo
    * ➜  blog git:(master) ✗ hugo server -D --bind=raspberrypi.local
    * [1]    6448 illegal hardware instruction  hugo server -D --bind=raspberrypi.local
  * Sooo I'm compiling this thing now.
  * and it's taking a while, just finding dependencies
  * let's see whether the battery makes it
  * after finding and downloading like 600 dependencies, it didn't work because it needs Go 1.14 but 1.10 is in the repos
  * took like 45 minutes just to get to that point
  * not gonna try compiling Go on the Zero... so let's cross compile https://www.thepolyglotdeveloper.com/2017/04/cross-compiling-golang-applications-raspberry-pi/
  * testing with a hello world:
    * using `GOARM=7` gives illegal hardware instruction. The article uses v5, which works, but the Zero's BCM2835 is actually ARMv6 (first released in 2002, by the way, and the 2835 is 65nm! just how little power would a 5nm equivalent need?) so that works too.
  * then running `env GOOS=linux GOARCH=arm GOARM=6 go build`...
    * firstly, it's like 3000 times faster on my desktop, done in less than a minute!
    * aaaand it actually works
    * takes 4615ms to build site while my desktop does it in 245

➜  blog git:(master) ✗ hugo
Start building sites … 

                   | EN  
-------------------+-----
  Pages            | 24  
  Paginator pages  |  0  
  Non-page files   | 19  
  Static files     | 11  
  Processed images |  0  
  Aliases          |  0  
  Sitemaps         |  1  
  Cleaned          |  0  

Total in 4615 ms

* Now to access it from the iPad:
  * get the `ip addr`
    * the one showin in iPad settings does *not* work
  * Run the server `hugo server --bind=169.254.154.185`
  * in Safari, go to `169.254.154.185:1313`


  

* This week
  * Hackintosh and work setups
* Next week
  * Taking notes, or: yet another Zettelkasten blog post
* After that
  * Accounting? Motivation, LSA book review and some PTA system?
  * Motivation:
    * Be prepared for emergencies
    * Recognize unneccessary spending
    * Save money consistently
    * Not directly necessary for everyone, but worth it if your financial situation is complicated

Other ideas. 

* Misinformation and reasoning by principles
  * Example?
* The merits of video games
* Fallout 3 on iPad (couldn't get it to work)
* On focus
* Accounting (plain text)

