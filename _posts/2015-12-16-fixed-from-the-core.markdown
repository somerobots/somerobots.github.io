---
layout: post
title:  "Fixed from the Core"
date:   2015-12-16 11:27:21
categories: news update
comments: true
---
*This is a technical post about the work that has gone into bringing you Trident v1.4.*

(v1.4 is not actually released yet! - waiting for review)

v1.4 was not a release for purely features, v1.3 had some serious bugs as I announced [earlier](http://somerobots.com/news/update/2015/12/02/Improving-Trident.html). Fixing these bugs involved auditing and rewriting huge parts of the app.

Apples Core Data (an 'object graph management' tool that can persist data to SQLite) is excellent. Core Data gives you a great set of tools to build your App with; a data modeling tool, controller classes like ```NSFetchedResultsController``` - which make it easy to observe changes in your dataset, a query language with ```NSPredicate```, I could go on. But one thing Core Data doesn't do well is thread easily. Well it *does* do threading, but you have to understand the rules. Starting a Core Data project requires knowing those rules and I think Apple could do much better at clearly outlining those rules in their documentation. Luckily, as I was writing Trident an [excellent](https://www.objc.io/books/core-data/) book on Core Data was being written which explains those rules.

Threading Core Data requires choosing a certain ['stack'](https://www.objc.io/issues/4-core-data/core-data-overview/) to enable importing data in a background thread, and observe those changes on the main thread. There are many options of possible 'stacks' you could build - but the choice required for you to take (there is no default Core Data stack!). You will find many references on the internet about the ```Confinement``` stack for Core Data - this is a now deprecated in iOS 9 and should not be used for new projects. Apple [recommends](https://developer.apple.com/library/tvos/documentation/Cocoa/Conceptual/CoreData/Concurrency.html#//apple_ref/doc/uid/TP40001075-CH24-SW2) a parent/child context stack - this is the typical stack I think many people use for modern Core Data projects. Apple also [recommends](https://developer.apple.com/library/mac/samplecode/Earthquakes/Introduction/Intro.html#//apple_ref/doc/uid/TP40014547) another stack option using two ```NSPersistentStoreCoordinator``` - this is the approach Trident v1.4 uses to import data.

You're probably wondering, why did I choose a two ```NSPersistentStoreCoordinator``` stack, and what is it? Trident imports lots of data in the background - I wanted to find the best way to do this. The two ```NSPersistentStoreCoordinator``` stack involves creating two ```NSManagedObjectContexts```, one with the ```MainQueueConcurrencyType``` and other other with ```PrivateQueueConcurrencyType``` - each context connects to their own independent ```NSPersistentStoreCoordinator```. The reason why this approach is great is because  in typical singular coordinator setup, only one context can access the coordinator at a time - this creates contention at the coordinator level. Creating two coordinators defers that to the SQLite level, which is single writer multi reader. This means the main thread context now is free to read the SQLite even during a large update is happening. The Core Data book I mentioned goes into much more detail than I have explained here, particularly about the advantages and disadvantages of this approach.

I hope reading this helps you if you too are suffering from Core Data problems!
