---
layout: post
title:  "SciOp Raspberry Pi Torrent Box"
date:   2026-10-18 19:00:00 +0100
tags: raspberry pi, linux, torrent, torrenting, SciOp, antifascist, antifa
---

[quote from sciop]

I've recently been having some fun setting people up with Raspberry Pis (tiny computers) which can contribute to the collective efforts of SciOp.
These little devices can sit in a cupboard and quietly contribute to a vast distributed storage network for threatened data.

I've particularly enjoyed the challenge of doing this with a mindset of minimising e-waste (which is linked to a "degrowth" philosophy in my mind), and so I have a goal of not buying anything new for these projects.
Thankfully, my house-mate was recently gifted an assortment of old Raspberry Pis from a research lab which was shutting down, and so I've had some to play with!
Add to that an old box of SD cards and memory sticks and some USB power supplies and we're off to the races.

I've got a 3B+ up and running at home, but there are a few very old models which I wanted to see if I could do anything useful with.
They're quite underpowered by today's computational standards, and so doing many of the [projects that people often use Raspberry Pis for](https://projects.raspberrypi.org) is a bit challenging.
Might they have _just_ enough umph to run a torrent client though? Turns out - yes!

At some point I'd love to create a neat "image" (so that folks could just download a thing, put it on an SD card, turn on the pi and be good to go), but until I work out how to do that, here's some instructions.

These are specifically for a Raspberry Pi XXXXXXXXX, though similar instructions will apply to other models. Tweak the OS accordingly, and it should just work[^1].

_Note: I used an LLM to help me work out how to do this. This worked for me, and I hope it works for you, but it comes with zero warranty._

## 1. Install an OS

My main laptop runs Windows 10 (for now...), and so I used the Windows version of the [Raspberry Pi imager](https://www.raspberrypi.com/software/).

Through a bit of trial and error I found that the two Raspberry Pis I have don't like micro-SD cards in an converter, and only seem to be happy with an actual full size SD card. I can find no reason for this to be the case, and yet it does seem to be the case :shrug:.
So, I sacrificed and old SD card which has a retro games emulator on it (sad crying face) and imaged it with XXXXXXXXX.
The older Raspberry Pis need the 32-bit images, and since we're going to be tight on CPU and can get away without a GUI we can go for the "lite" version which does not have a graphical user interface. XXXXXX old OS? XXXXXX

I set a hostname (something like "scioptorrentbox"), a username (something like "danny"), and a password (something like... haha jk jk. But seriously, probably wise to keep it alphanumeric for this - I had some issues recently which boiled down to having fun characters in passwords on a pi). I keep wifi off (this device doesn't have it), and ssh on (which we'll use later).

## 2. Put the SD card into the pi, and turn it on

To be safe, I like to connect the power cable to the pi side first, and then to the power provider, just to minimise the chances of [shorting something](https://social.coop/@da5nsy/116824280369217307).
It's probably also wise to get a case to further reduce the chances of this, or, as I do, use an old take-away container. This does not align with my housemates interior design aspirations, but it works.

## 3. Access the pi via `ssh`

Now, at this stage you can either plug in a screen and a keyboard, or you can be a **super cool hacker** and `ssh` in. 

[HACKERS GIF]
[MATRIX GIF]

On another computer, which is connected to the same router (by wifi or ethernet), open a terminal window[^2].

Run:
```
ssh [user]@[hostname].local XXXXXXX
```
(E.g. in my case, it would be `sss danny@scioptorrentbox.local` XXXXXXX)

It'll then ask for your password. Type it it, and don't be alarmed that you can't see it typing - it is, and then press enter.

It will say something about a fingerprint. Press enter again. XXXXXXXXX

## 4. Install qbittorrent

We need some software to download and upload torrents. This is normally used by teenagers around 2010 to pirate movies. I ([and SciOp](XXXXXXXXX) recommend qbittorrent.

For this specific project, I recommend "qbittorrent-nox". The "nox" roughly translates as "no screen". Since we have an OS without a desktop environment, and a computer that would struggle to put something on a screen _and_ do something simultaneously, the version without the screen output is the one to go for.

The simplest way to do this is:
```
sudo apt install qbittorrent-nox
```

That will get you qbittorrent-nox, but it will get you whatever the latest version was when your OS was released, so it's probably quite old.

If you encounter issues (like something in qbittorrent not working like you expect it to), try this instead, to install a more recent version:
```
sudo apt install wget
wget /usr/local/bin/qbittorrent-nox https://github.com/userdocs/qbittorrent-nox-static/releases/latest/download/armhf-qbittorrent-nox
sudo chmod 755 /usr/local/bin/qbittorrent-nox
```

Then, type `qbittorrent`, and hit enter, to run the program.

From another computer, open a web browser and navigate to `http://[user]@[hostname].local:8080`. XXXXXXXX [does this default to 8080?]

## 5. Add some torrents from sciop.net!

## 6. Set it to autostart on boot XXXXXXXXXXX [is there actually a way to do this within qbittorrent?]

Happy torrenting! 😇☠️

_If you see any way to improve this post, either [send me an angry email](mailto:dannygarside@outlook.com), or [submit a PR to my website directly](https://github.com/da5nsy/da5nsy.github.io ... XXXXXXXXX)._


[^1]: Famous last words... XXXXXXXXXX
[^2]: On Windows, type cmd into the search bar and hit enter. On Mac, no idea. On Linux... you have almost definitely been forced to use this on a daily basis since you switched to linux, but if not, open the Terminal app, or whatever exciting alternative you have.