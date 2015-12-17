---
layout: post
title:  "Trident gets notifications"
date:   2015-12-02 11:27:21
categories: news update
comments: true
---
With the release of Version 1.3, Trident can now fetch updates in the background and notify you of changes for your GitLab server.

This is very handy if you're involved in a project and you need to be updated for particular things, like issues, merge requests and Git pushes. The notifications are configurable in the settings area, so you don't have to receive every type of notification.

Because of the way this is implemented (using a feature added in iOS 8 - Background Fetches) - no changes are needed on your GitLab server to receive these notifications. However, there will be some delay between the event happening and you receiving the notification. The delay will depend on how much battery your phone has left, whether you've enabled low power mode, or if you don't frequently open Trident. If you force close the app you'll also not receive notifications.

<img src="{{ site.baseurl }}/assets/version14_images/Notifications.png" srcset="{{ site.baseurl }}/assets/version14_images/Notifications@2x.png 2x">    
