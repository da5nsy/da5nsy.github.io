---
layout: post
title:  "My Signal backup system"
date:   2023-09-09 09:00:00 +0100
tags: Signal backup open-source
---

_This is a "living" blog post. I will update it as my practice changes. Its history can be found [here](https://github.com/da5nsy/da5nsy.github.io/blob/master/_posts/2023-09-09-My-Signal-backup-system.md)._

I lost my phone a while back, which sucked.
One especially sucky thing was that I didn't have my Signal chats backed up.
Some people like to treat their messages as ephemeral. I don't. Not my style at all.
So I (now) have a backup system that runs automatically every night.

Here's how it currently works.
_Disclaimer: This setup won't win any prizes for security/privacy. That's not my priority. For some people, those are priorities. They probably won't like this set up[^1]._
- I turn on Signal backups
- Done! ✨ *LOL NO JK*. That just creates local backups, which is as useful as a ~~chocolate~~[^2] ***shit*** teapot if you lose your phone.
- I then have an app called Foldersync[^3], which does what it says on the tin.
- Specifically, it syncs local and remote folders, including cloud storage services.
- I have mine set up to sync to my Dropbox overnight every night. One directionally, so it only adds files, doesn't delete.

And that's it! If it works as anticipated, I should never again lose my messages.

One thing I would _love_ though, is if I could just store the diff between days.
Each backup file is 1GB and it just feels wasteful knowing that 99% of that file is a duplication.
Presumably whatsapp does something like this?
I guess a solution would be an a pipeline that does automated on-phone decryption (or just accessing an unencrypted storage directly, if that exists?) and then a git commit and push.
That seems like an awful lot of effort though...

I'd also be interested in FolderSync alternative - it works fine, but I'd prefer an open-source tool ideally.

If you have ideas about how to improve this system, please do get in touch via [email](mailto:dannygarside@outlook.com) or [mastodon](https://social.coop/@da5nsy)! 🙏

[^1]: If there are easy ways for me to improve the security of this system, let me know please.
[^2]:  At least a chocolate teapot creates a *tasty* mess...
[^3]: [https://foldersync.io/](https://foldersync.io/)

