---
layout: post
title:  "Making a Hugo website, hosted on Codeberg, and pushing to a Web Architects server"
date:   2026-01-01 19:00:00 +0100
tags: housing co-ops, tech, software, Hugo, codeberg, website, tech co-ops
---

I'm involved in starting a housing co-op, and as of today we have a (shitty placeholder) [website](https://perennialhousingcoop.uk/)! :tada:

I wanted to have it hosted by [Web Architects](https://www.webarchitects.coop/) because they're a cool tech co-op doing good thing, and also because then I could copy the system that we use over on [Corvus Co-op](https://corvus-coop.org/). [Jez](https://erambler.co.uk/) (who set up the Corvus Co-op website) lent me a hand, and along the way taught me what SSH was, which was a whole lot of fun. I am now unstoppable.

Here's my notes in case I/you/whoever wants to do the same again.
Not all of these are necessary.
Note: I'm on Ubuntu 24.04.3 LTS, with many things installed already (git, hugo,...) so if you're doing this fresh you may need to install bits! 

1. Give [Web Architects](https://www.webarchitects.coop/) some money

In order to register a domain they'll ask for various address and ID info, send you and invoice, and do some domain registration stuff in the background.
Then they'll send you some SSH credentials.

2. [Set up a codeberg repo](https://codeberg.org/repo/create), and initialise it with a readme or something like that.

3. Do a local git clone and initialise a Hugo project

Following instructions from: https://gohugo.io/getting-started/quick-start/

-`hugo version`
    - hugo v0.152.2-6abdacad3f3fe944ea42177844469139e81feda6+extended linux/amd64 BuildDate=2025-10-24T15:31:49Z VendorInfo=snap:0.152.2
- `git clone https://codeberg.org/da5nsy/perennialhousingcoop`
- `cd perennialhousingcoop/`
- `hugo new site . --force` (`--force` because it is not an empty folder)
- `git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke`
- `echo "theme = 'ananke'" >> hugo.toml`
- `hugo server`
    - Open a browser and see a local preview of the site.
- Update `hugo.toml` with the right title and URL etc.

4. Check your SSH access works

- ssh into WebArch - `ssh perennial@webarch1.co.uk`
- add a html and check it works - `touch index.html`
- add some test text - `echo "this text" > index.html`
- add a copy of the hugo build manually
    - `hugo` (locally)
    - `scp -r /home/danny/Documents/perennialhousingcoop/public/* perennial@webarch1.co.uk:sites/static/`
    
5. _(Get a quick primer from [Jez](https://erambler.co.uk/) on what SSH is)_

- public and private parts
- public encrypts, private decrypts
- never share the private part

6. Set up local SSH access to Web Architects so that you don't have to enter the password every time

- `ssh-keygen`
- `ssh-copy-id perennial@webarch1.co.uk` (this copies your computer's default SSH to webarch)
- `ssh 'perennial@webarch1.co.uk'` (test it works)

7. Make the website build on Codeberg

- copied https://codeberg.org/corvus-coop/pages-source/src/branch/main/.forgejo/workflows/build.yaml into the repo
- activated actions on the repo (https://codeberg.org/da5nsy/perennialhousingcoop/settings/units)
- did a test `git push` to get the action to run
    - build successful
    - deploy unsuccessful (as expected, because we haven't given the Web Architects server any reason to trust this repo yet)
- add variables (https://codeberg.org/da5nsy/perennialhousingcoop/settings/actions/variables)
    - copied from https://codeberg.org/corvus-coop/pages-source/settings/actions/variables , changing Corvus -> Perennial etc.
    
8. Make the build website get pushed to the Web Arch server. 

- generate a new (different SSH key) to give to codeberg (so that WebArch knows to trust this codeberg repo)
    - `ssh-keygen`
    - "Enter file in which to save the key (/home/danny/.ssh/id_ed25519):" `/home/danny/Documents/perennialhousingcoop/id_ed25519`
    - Add `id*` to the `.gitignore` file (so we don't accidentally commit our secrets)
    - `awk '{printf "%s\\n", $0}' < id_ed25519` (textual representation of key)
        - copy this into https://codeberg.org/da5nsy/perennialhousingcoop/settings/actions/secrets as `DEPLOY-KEY`
    - from danny@hades:~/Documents/perennialhousingcoop$ `ssh-copy-id -i id_ed25519 perennial@webarch1.co.uk` (this copies the key which is in the repo, rather than the computer's default one which also has the same name)
    
9. Wrapping up

I also needed to [enable submodules](https://codeberg.org/da5nsy/perennialhousingcoop/src/commit/681f4070c5095a082f0c03d15877e601b68a70b2/.forgejo/workflows/build.yaml#L10-L11) in the build. Corvus Co-op [uses a different way of importing the theme](https://codeberg.org/corvus-coop/pages-source/src/commit/d087e4e8201222245989b0f4c64d410231adfa69/hugo.yaml#L36-L38), which maybe longterm is actually better, but I used the hugo reference docs so I'll stick with that for now.

And just like that... we have a ~~beautiful~~ draft website.
Thank you [Jez](https://erambler.co.uk/), the Web Arch folks, the Hugo folks, the Codeberg folks, all the other open-source maintainers... you get the idea! 🙌


