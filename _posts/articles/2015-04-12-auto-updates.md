---
layout: post
published: true
tags: [easymark]
category: articles
excerpt: In which I ponder usability
title: There's an update available, install now?
---

As I was working on [my markdown
viewer](https://github.com/joukevandermaas/easymark), I realized it needed
automatic updates.  My plan is to keep releasing incremental improvements.
Since I cannot expect people to be excited about something as mundane as a
markdown viewer, auto updates are a must.  As I was considering how this should
work, I went over some of the existing auto update strategies I've seen used. 

# Show a message, send to download page

The absolute bare minimum one can do is to just notify the user of an update.
Many applications do this: they simply tell you there's an update and open the
download page (or project home page) in your browser. I barely consider this a
real option, since I *never* download updates for these apps. I'll be using
myself as an example user for most of these posts, since I'm going to be the
primary user for the foreseeable future.

# Simple confirmation with an installer

The next simplest and probably most common form of 'real' auto update is a
simple 'new version available, update now?' box when the app starts. I have
several problems with this approach. First of all, when I start an app I mean
business. It is the worst possible time to interrupt me, especially if you're
going to then show me an installer with several steps. I would not start the
app if I didn't want to use it *immediately*. 

One simple way to improve on this would be to move the message to the end of
the session. When I close the app, I'm done: there is no work to interrupt at
this point. Given how simple it is to just download the newest installer, this
solution may be a good candidate for early versions of the viewer. 

# Update in the background

The final option I have seen is both the simplest (from the user's perspective)
and the most difficult (from the programmer's perspective). This is the model
used by applications like [Chrome] and [Spotify]. From the user's point of
view, the application is simply always up to date. There is no special action
required by them, save maybe restarting the app every now and then. While there
are some potential downsides (e.g. you can't keep using an older version
without manual effort; the app probably needs to be installed in a subfolder of
the user directory), the simplicity of the solution easily outweighs them.

# Making a choice

While I really like the third option described above, it's the most effort from
the programmer's perspective (me in this case..). At this stage of the
application, I'd rather focus on adding more directly beneficial features, than
to take away a very minor inconvenience. Since the app will have some form of
auto-updates, I'll be able to improve on it later, when the feature set is more
complete. This is why I have chosen to go for the simple solution described
above.


[Chrome]: http://www.google.com/chrome/
[Spotify]: http://www.spotify.com
