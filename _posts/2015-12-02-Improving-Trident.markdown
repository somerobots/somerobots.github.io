---
layout: post
title:  "Improving Trident"
date:   2015-12-02 11:28:21
categories: news update
comments: true
---
Trident 1.4 <strike>(the next version as of writing)</strike> is going to be a big update, the features I expect to add will be (but not limited to):

- Markdown support for issues and merge requests
- Emoji suport
- Assign issues to Team members and to anyone else on the GitLab server
- View Tags and Branches (showing protection state)
- Goto Merge Requests from the History feed
- Goto Git Push events from the History feed

The big push for 1.4 though is an emphasis on **quality**, **stability** and **speed**.

Sytse from GitLab very kindly allowed me guest access to GitLab CE for me to test Trident on. Trident positively melted with the volume of data in this repo. I didn't realise it was that bad until I saw this.

The issue affecting Trident is a dreaded threading issue, Trident uses ```Core Data``` to cache data from GitLab - which is quite a complex beast to thread correctly. Trident also has a massive entity model (the biggest I've ever personally worked on).

There is a golden rule in ```Core Data```, only access data on the thread that created the entity. Trident broke that rule - often. Using information from [Core Data Concurrency Debugging](http://oleb.net/blog/2014/06/core-data-concurrency-debugging/) has really helped. Trident can now handle data from GitLab CE and now I use Trident to keep up-to-date with GitLab CE changes! Handy 😀

There are however still more issues needed to fix to make Trident deadlock free. There is presently an issue with ```NSFetchedResultsController``` deadlocking with its ```performFetch```. I'm not sure yet what is causing this, if it is a symptom of a problem elsewhere or whether it is a problem with the controller. At least encouragingly, the app no longer (as far as I can see), accesses data on the wrong thread. I will continue to work hard on this issue until it is fixed.   
