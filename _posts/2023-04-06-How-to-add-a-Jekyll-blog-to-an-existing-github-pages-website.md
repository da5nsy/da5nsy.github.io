---
layout: post
title:  "How to add a Jekyll blog to an existing github pages website"
date:   2023-04-06 09:00:00 +0100
tags: Jekyll blog github-page
---

Yesterday I added a blog to my website. I couldn't find clear instructions for doing this, and I ended up going down several dead ends, so here's what worked for me.

I already had a [website](https://web.archive.org/web/20230313161905/http://www.dannygarside.co.uk/), which was very simple (pretty much just a [single html page](https://github.com/da5nsy/da5nsy.github.io/tree/57054fbaedcccba7a9f12a76835fa4d96db724e4)), but I recently started wanting to write a blog. I'd previously written some things on Medium, but I wanted to move away from using a third party, and I figured "how hard could it be to make one on my website?". Spoiler: it took some faffing. 

Jekyll seemed like a sensible option, so without much further thought I dove in.

I work on Windows, so following [these instructions from github](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll), and then [these instructions from Jekyll](https://jekyllrb.com/docs/installation/windows/) I installed Ruby+Devkit.

Since I already had a clone of [my repo](https://github.com/da5nsy/da5nsy.github.io) locally I could skip straight to point 7 of [the github instructions](https://web.archive.org/web/20230328231910/https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll) (_I'm linking to the web archive version of the instructions, just in case they change_): 
- `jekyll new --skip-bundle --force .` (`--force` is needed because jekyll expects an empty repo)
- Opening [the Gemfile](https://github.com/da5nsy/da5nsy.github.io/blob/a4afcb274d1fee648246f154178e4422a217f3ab/Gemfile) in a text editor (I used Notepad++)
	- Comment out line 10 `# gem "jekyll", "~> 4.3.2"` in the Gemfile
	- Modify line 15 to `gem "github-pages", "~> 228", group: :jekyll_plugins` (checking the version [here](https://pages.github.com/versions/))
- `bundle install`
- Modify the config file. For me the important part was: `url: "https://www.dannygarside.co.uk"`

Then to test my site locally I continued with [these instructions](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll#building-your-site-locally) and ran:  `bundle exec jekyll serve`. At first it threw an error (`cannot load such file -- webrick`) which I resolved with `bundle add webrick` ([info here](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll#building-your-site-locally)), and then it worked!

Well, it sort of worked, in that it showed my original site, and if I went to `http://127.0.0.1:4000/blog/` it showed a 404...

To tell Jekyll that I wanted to keep my original home page, and that I wanted to have the blog at `dannygarside.co.uk/blog` I did the following:
- added this line to the config file: `permalink: /blog/:title/` (this also makes it so that the URL for each blog is just the title, rather than the date and title, which I prefer).
- Copied my previous html homepage into a new folder (`_layouts`) and renamed it `home.html`.
- Added `blog.html` [to my root directory](https://github.com/da5nsy/da5nsy.github.io/blob/af85f3a2935bfd8813efe47f85936239400d2310/blog.html). I honestly don't remember where from, somewhere near [here](https://jekyllrb.com/docs/step-by-step/04-layouts/) I think...

**And that was all the heavy lifting done!** &#127881;

<br>

## Extras

I then did a couple of snazzy extra things like:
- [Added a custom font](https://github.com/da5nsy/da5nsy.github.io/commit/af85f3a2935bfd8813efe47f85936239400d2310#diff-3a56bfc93d029f425c8fbd43b763c034935c43cea022202ea319c19555a7eb8a)
- [Increased the default size of the font](https://github.com/da5nsy/da5nsy.github.io/commit/8a59e3f76ca67492d4a82b1e94d48a22afc954b6)
- [Added a gradient background](https://github.com/da5nsy/da5nsy.github.io/commit/edea7baa78b661f5f178ab1e539d857a4bc08a32)


