---
layout: post
title:  "Housing Co-op Tech"
date:   2025-09-10 09:00:00 +0100
tags: co-op, tech
---

_This is a live post - I may update it. Check the [git history](https://github.com/da5nsy/da5nsy.github.io/commits/master/_posts/2025-09-10-Housing-co-op-tech.md) if you want to see what was said in previous versions_

I've wanted to tell a few people about the tech we're using for Perennial Housing Co-op (don't look it up, there's nothing public yet, but there will be "soon"! ✨ tl;dr I'm part of a group setting up a Radical Routes housing co-op in NE London) recently, because I spent a while working it out and while it's not perfect I think it's relatively rad.

My guiding principles were: 
1. fuck Google
2. ... and _all the other fuckers too_

So, I wanted open-source tools, ideally hosted by other co-ops. 
And ideally in a way which would mean that I wouldn't pull my own hair out trying to use them, and recognising that the capacity for "determined button pressing"™️ is lower among some of my housing co-op comrades than it is for me. I'm the sort of person who accidentally joins the Digital working group of Radical Routes because I wanted to fix a typo on the website and now I think I'm several steps down the path to becoming a sys admin (to be clear: I have no idea what I'm doing).

So, we need[^1] a few things to be able to operate as an organisation in the modern world:
- a place to chat (send memes etc.)
- a digital address that people _not_ in our ~~cult~~ club can contact us through (an "email address")
- somewhere to put documents that we're working on, ideally somewhere we can simultaneously edit them together through a browser (isn't it wild that this went from "not a thing. Are you ok?" to "obviously this is normal and needed" within a few years!?)
- a calendar ([insert quip])

## Chat

For chatting I am a big ol' **Signal** fanboy - it's like WhatsApp but not owned by fuckers.
It's a jolly cool non-profit that is very good at fancy things like encryption which mean your texts don't get used in court against you one day. 
I think it's open source too (go check for yourself if this is important - I'm writing this on a train with crap wifi).
I was at a workshop a while back which made a suggestion which has stuck with me, along the lines of: "use the encrypted chat for organising your film nights, so that when you need to use it to organise your rebellion all your comrades already have it installed".

We also have a **Zulip** - this is like Slack or Microsoft Teams but again (you guessed it...) not owned by fuckers.
This has threaded communication, which I think might be handy for when we have 10 different conversations happening simultaneously.
Could we just use Zulip and not Signal as well? Probably. Are we doing that? Probably not. 
The other open-source tool in this space is Mattermost, which I've had good experiences with (we use it at the [Digital Research Academy](https://digital-research.academy), but Mattermost seems to not have a free hosted option, whereas Zulip kindly offers free hosting for small (less than 5GB I think) instances, and seems to be very friendly to open-source software projects and academic research projects. Mattermost OTOH seems to be a bit more corporate in nature.

A note at this point: **pay for your open-source software**. 
I'm glad that Zulip offers free hosting for small accounts, because we don't have our finances worked out yet, and it gives us a chance to try it without having to sort out our finances, but long-term ***we need to support the things we want to see thrive*** and while we exist under capitalism this means ***giving them money*** (I have a whole 'nother blog post languishing in drafts about this). 
That means giving money even when you are not forced to, which some people sometimes call "donating", but which I like to think of as organisation-level-mutual-aid (thanks to the friend who coined this recently - you know who you are).

## Email

E-mail is a tough one - if you don't pick one of the big guys you end up getting blocked left, right and center.
But we figured we'd give it a go.
We managed to get an invite to riseup from a friend (they're invite-only currently, and only for activisty types).
Send us jokes pls: perennial@riseup.net

## Docs

We briefly had a Google Drive and I hope that God will forgive me when my time comes.
I then spent a long time looking into Nextcloud and eventually concluded that it looks pretty cool but we'd have to pay a solid chunk of cash for it and it was probably more eavyweight than we needed - we're not writing our theses, we're just jotting down some meeting notes [^2].
In the end (for now) we settled on CryptPad - this is a super secure (way more secure than we need, but hey ho) "pad" (things like etherpad and hedgedocs) and also a "drive" like Google Drive where you can store a bunch of different files in a directory structure.
You can upload any format you want, but a subset of those files will be edittable in the browser.
I think we pay some money for this, but I think because I wanted to rather than because we had to for a specific feature (perhaps I wanted some "faster support" at some point?)

## Calendar

Y'know how I mentioned that Cryptpad was more secure than we need? This includes having a calendar system which is so secure that you can't invite people to your events. So we opted for _not that_.
Instead we decided to actually use a Nextcloud host - https://thegood.cloud/. That's right - Nextcloud includes a calendar system. "Why not use Nextcloud for both files and calendar?" I hear you say! Well, https://thegood.cloud/ offers a free tier but you can't have shared drives at that level, which means we can't really do collaborative editing with it. So... we have a single free account on https://thegood.cloud/ just for calendar purposes, which we can all log into (or set up Thunderbird etc. to edit the events indirectly - though, note: how to set that up was not obvious...) and stick with cryptpad for docs.

## Video-calls

Sometimes we want to meet and argue about decision-making processes and our own personal opinions on how best to bring about the downfall of capitalism, but we can't find a time where can all meet in person because we're busy London millenials with social calendars which make eyes bleed.

So, having a "place" where we can "meet" digitally is handy.
I personally have access to [meet.coop](https://meet.coop) through [social.coop](https://social.coop) ([info](https://wiki.social.coop/wiki/Tutorials#Using_partner_platforms)) AND through [Radical Routes](https://www.radicalroutes.org.uk) so, we're rich in meet.coop accounts, but in practice quite often someone's computer won't connect to the audio or there's some other bug, and so we switch to calling through Signal which we have anyhow and which works more reliably though it's a bit less feature rich.

## Conclusion

So, that's everything. 
I'll update this when I remember things I've forgotten or people ask me questions about it :+1:

[^1]: Do we ever really "need" anything?

[^2]: If we _do_ go down this route in the future we'll be getting it hosted by [Web Architects Co-op](https://www.webarchitects.coop/) or [Autonomic Co-op](https://autonomic.zone/), both of whom seem lovely and rad. And then we can probably get them to host versions of all the above for us, and possibly even do SSO, which would make things a whole lot easier.

