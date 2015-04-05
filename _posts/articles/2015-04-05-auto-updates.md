---
layout: post
title: There's an update available
published: false
---

# There is an update available
As I was working on my markdown viewer, I realized it needed automatic updates. My plan is to keep releasing incremental improvements, so I could get something out there early and improve based on usage, rather than design the whole thing up front. Since I cannot expect people to be excited about something as mundane as a markdown viewer, auto updates are a must. 
As I was considering how this should work, I went over some of the existing auto update strategies I've seen used. 

## Show a message, send to download page
The absolute bare minimum one can do is to just notify the user of an update. 

## Simple confirmation with an installer
The simplest and probably most common form of ’real’ auto update is a simple ’new version available, update now?’ box when the app starts. I have several problems with this approach. First of all, when I start an app I mean business. It is the worst possible time to interrupt me, especially if you're going to then show me an installer with several steps. *I would not start the app if I didn't want to use it immediately*. 

One simple way to improve on this would be to move the message to the end of the session. When I close the app, I'm done: there is no workflow to interrupt at this point. Given how simple it is to just download the newest installer, this solution may be a good candidate for early versions of the viewer. 

## Update in the background, require restart
Another update strategy I've seen used, most notably in spotify, is to download the newer version in the background, and then ask the user to restart the app. This is far less invasive than the models above, but i still have several problems with it. 

First of all, if you can download in the background, why ask the user anything at all? Why not just wait for the user to close the app (as they inevitably will) and perform the copy then? By giving the user a prompt or banner, you give them the illusion of choice, when really they have none. 

That said, 

