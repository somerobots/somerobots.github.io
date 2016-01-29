---
layout: post
title:  "Back on track for next release"
date:   2016-01-12 11:27:21
categories: news update
comments: true
---
Earlier I wrote about [v1.4.1](http://somerobots.com/news/update/2015/12/31/dashboard-improvements-and-2fa.html), however due to a bug discovered during the TestFlight the release was delayed - GitHub 2FA Authentication wasn't working correctly (shout out to Ariel Elkin for discovering this 👍).

In the process of delaying the release, more bugs and issues were discovered. A big shout out to Thomas Hartwig for his [UX improvements suggestions](https://gitlab.com/somerobots/Trident/issues/124) to the Project Selector, having made a mockup for his improvement suggestions was really cool 😎, GitLab project avatars are now shown. Thomas also solved some issues with the [app navigation](https://gitlab.com/somerobots/Trident/issues/126) by moving the host selection out of the Settings Tab and into the [modal window](https://marvelapp.com/bgbjhj). The host selection changes are going to happen in the next release!

This release also adds an early preview for [iPad support](https://gitlab.com/somerobots/Trident/issues/123), more work is needed to fully use the layout of the iPad, which I anticipate to see some progress in the next release with some Master / Detail and layout changes.

I'm happy to say v1.4.1 is now back 'waiting for review' again, I went a bit mad and expanded the scope of this release, the full change log is as follows:

- Added support for iPad.
- Added support for landscape.
- Added support for GitLab Project Avatars.
- Added support for GitLab [starred projects](https://gitlab.com/somerobots/Trident/issues/50) (only available in GitLab 8.3+ hosts).
- Added support for GitHub 2FA.
- Added support for GitHub Pull Requests.
- GitLab login now shows HTTPS toggle - incase you're not using SSL.
- Improved darkmode, it's now App wide!
- Improved the dashboard, goto issues, merge requests and git pushes, straight from the dashboard!
- Improved history screen, even faster loading of comments.
- History and Dashboard now support lazy load issue and merge requests.
- Fixes issue with central spinner showing incorrectly.
- Increased height of tab bar slightly (48pt).
- Markdown is cached (in-memory) for speedier scrolling.
- Fixes some performance issue when switching tabs too often.

Looking forward to v1.5 now 😎
