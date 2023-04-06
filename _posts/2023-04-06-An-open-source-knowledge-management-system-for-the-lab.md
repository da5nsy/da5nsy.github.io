---
layout: post
title:  "An open-source knowledge management system for the lab"
date:   2023-04-06 17:00:00 +0100
tags: KMS knowledge-management-system logseq
---

_This blog is adapted from an informal talk I gave at the [Open Science Retreat](https://open-science-retreat.gitlab.io/). Thanks to those who joined!_

Last summer two things happened in quick succession - the NIH mandated that we stop using paper lab notebooks, and my PI found an issue in some data that that had been collected and pre-processed ~10 years ago. 

Something had been done wrong during the preprocessing, but of course the people who had actually performed this preprocessing were long gone, and there were no clear notes on exactly what preprocessing had been performed. My PI spent a great deal of time trawling through archives and old emails to understand what had happened, and everything worked out in the end, but it wasn't a fun experience for anyone.

And so my PI turned to me and said something along the lines of _"Hey Danny, you're interested in this lab infrastructure stuff, and reproducibility, can you look into something that could replace lab notebooks, and also mean that I never have to do that again?"_.

I'd been trying out different note taking systems for a while (my PhD notes are one very long ms word document...) and I'd recently become interested in "second brain" systems, like obsidian, logseq, Roam Research, Athens Research etc.

With these the idea is that everything is put onto "paper" with lots of cross-references, which turns out to be rather intuitive and satisfying for many people, and can make it easier to recall information quickly and reliably. 

You also get pretty graphs like this that show the various connections between all the things you've been thinking about.

![](https://cdn.fosstodon.org/media_attachments/files/109/842/611/209/569/624/original/85df26571294934a.png)

Of the available options I personally prefer logseq, because it is open source, and the underlying files are just markdown files, and so you're not locked into the system at all - it would be fairly easy to pick up your stuff and move to a different system.

I won't go too deep into the general usage of logseq, because there are [many places that do that well already](https://hub.logseq.com/getting-started/uQdEHALJo7RWnDLLLP7uux/how-to-get-started-in-logseq/pE1BPPvKGbWkSRXsprRnxM). But in a sentence: you write notes as nested bullet lists, generally on dated journal pages, and it is very easy to cross-reference to other pages and even specific bullet points.

The downside is that it is not set up to be used collaboratively by multiple people, so that took a little bit of tinkering.

## Technical solution

The bulk of the technical solution can be summarised by the contents of this `.gitignore` file.
```
logseq/*
journals/*
*.DS_Store

# but don't ignore this file:
!logseq/config.edn
```

I created a git repo and started a logseq graph in it, and then told git to ignore the `logseq` folder (where user settings are stored), the `journals` folder (because otherwise multiple users would have filename clashes whenever they wrote things on the same day), `DS_Store` files (because mac users), and then _don't_ ignore `logseq/config.edn`. This last command is in place so that everyone uses the same date format.

## Social solution

The other part of the solution was social - asking people to use the system in a specific way that would allow all of our notes to co-exist and interact without issue.

They key element was asking people to all use a standard page title format, and to avoid using the built-in journal pages. My proposed format was `YYYY-MM-DD/Name`, which ensures that everything is date ordered, even if you're just ordering it alphabetically in a file browser, and should avoid clashes. What happens when we have two people in the lab with the same name? We'll cross that bridge when we get to it.

Coupled with frequent tagging of projects, people, and equipment, this should mean that it will be fairly easy to quickly look up almost anything on the fly at a later date!  &#129310;

<br>

## Extras

**Q: What do you keep in there? What don't you?**

A: We're still working this out but as a basic rule of thumb: anything that would have gone into a paper notebook. This mainly includes metadata about data collection: how many runs were collected, which run had to be aborted because X piece of equipment needed rebooting, etc. I personally use it for a much greater range of things than this, because that's how my mind works: I find it easier to keep track of my thoughts if I'm writing them out, and so I write notes while I'm coding, or reading papers, or thinking through experimental design or analysis questions.

**Q: Wouldn't it be better to keep the notes next to the data, on a project-by-project basis? What about existing projects that already have a repo with a sidecar logbook?**

A: We're trying out a compromise solution for this currently: for projects that have existing repos, or where there's a very good justification for keeping the notes directly alongside other assets, we add those projects as a [submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) to our logseq repo. Then we can either add the large/private assets to the gitignore of that repo, or do a [sparse checkout](https://git-scm.com/docs/git-sparse-checkout) when we're checking out the submodule into the logseq repo. Then other users get the choice whether to add those notes to their specific instance of the logseq repo.

**Q: What about when you're collaborating with others? Do you force them to use this system for their notes?**

A: No. Though if it's useful we can give them access to our logseq repo, so that we can send them links to specific pages (_"hey checkout this super cool analysis I just did" etc_), and it's even nicer that github renders this markdown well, complete with embedded images.

**Q: Why use this system rather than something like [eLabFTW](https://www.elabftw.net/)?**

A: eLabFTW looks awesome (thanks Lukas for telling me about it!) and I can see how it would be useful for certain research groups. It looks like the technical onboarding ramp would be gentler (no need to know markdown or git), and for certain types of scientists it seems really well set up to integrate things like chemical diagrams, but for us we preferred to use a system that uses markdown under the hood, for greater ease flexibility down the road.
