---
layout: post
published: false
comments: true
tags: [ember]
category: articles
excerpt: On the various components of Ember and how they relate
title: Getting started with Ember.js: Part 1
---

[Ember] is a javascript framework for creating single page applications in an
easy and guided way. It has been around for a while and is relatively stable,
but the preferred way of building applications has shifted somewhat as the
Ember team has been preparing for the release of version 2.0 of their
framework. As a result of this, it is not always clear which parts are 'safe'
to use, and which you should avoid going forward. In this series, I'll attempt
to explain the fundamentals of Ember to allow you to get started building your
application.

[Ember]: http://emberjs.com

# Get Set Up

You will need at least [Node.js](https://nodejs.org/) (and npm) installed
before you can do anything else. To get started after that, execute the
following commands:

    npm install -g ember-cli
    ember new my-app

This will take a long time, because npm is slow. When it's done, you'll have
some 25,000 files most of which you don't care about (but still need for some
reason). What we're talking about today mostly concerns the `/app` subdirectory
in the root of your project. In a future post, we'll go into what everything
else is for.

# Parts of a Typical Ember App

Before we get started building something, let's go over the various moving
parts of a typical Ember application so we have some idea of what we're talking
about. I'll name and explain important concepts and when you should think about
using them. Note that all of these things can be generated using [Ember CLI]
blueprints; simply type `ember help generate` for an overview of what you can
do.

The goal of these posts is not to teach you everything there is to know about
Ember. Instead, I want to give you enough of a foundation so you can read other
blog posts or the official guides and more or less know what to do.

[Ember CLI]: http://www.ember-cli.com/

## Templates 

{% raw %}
The most obvious part of any Ember application is its templates. These are
declarative html-like descriptions called HTMLBars (or Handlebars) of how your
application should render. Dynamic parts are typically enclosed in double curly
braces like this: `{{hi i'm dynamic}}`. Dynamic blocks with html in the middle
work like this: `{{#somethingsomething}}<div>hi i'm
html</div>{{/somethingsomething}}`.

They can do all the things you'd expect from a modern templating tool, such as
`{{if` and `{{each`. The most interesting thing is that you can add your own
dynamic bits, in the form of (sub)routes, components and helpers. Keep in mind
that you cannot call arbitrary javascript from templates. Templates in Ember
are strictly declarative. 
{% endraw %}

## Routes

Everything in Ember starts with a route. Routes are conceptually a map between
the url and what is shown on the screen. They're the first way you're going to
split your application into smaller pieces. A good rule of thumb to use is to
create a route if it makes sense to be able to link to that state in the
application. For example, the edit tab on a user's profile might have the route
name `user.edit` which translates to the link `user/<id>/edit`. From this
example we can also see that routes can have arguments.

Since routes are the most top-level way to divide your application, almost
everything else will occur in the context of a route. Because of the way Ember
is set up however, information about the current route is not always available
everywhere. You should almost never do anything with a route, except to link to
them.

{% raw %}
Routes have an associated template, which renders 'somewhere' on the page. You,
of course, control this 'somewhere'. When you put `{{outlet}}` in your
template, that is the spot where a subroute will render. Ember adds on top of
this the idea of an *application*, which has its own template (but no route).
If this template does not have an outlet, nothing will render. So toplevel
routes (such as `index`) will render in the application template's outlet.
Subroutes render in their parent route's outlet, if it exists.
{% endraw %}

The bit where you put your logic and event handling is called a *view*. The bit
where you put your html markup is called a *template*. Apart from these two
things, routes need to be defined 'globally', typically in a file called
`router.js` in your app's root directory if you use Ember CLI.

## Components

Components will contain small bits of your application that you can reuse in
multiple places. For example, list items in a complicated view, or your login
form could be components. You can include components in any template, including
other component's. You can also pass arguments to components. This allows you
to encapsulate some logic in a very simple way.

Be careful about overusing components; they are no replacement for routes
(yet). If it makes sense for a user to link to a state of the application (like
the active tab described above), you should use subroutes instead of
components.

{% raw %}
To include a component in your template, simply put it in handlebars:
`{{my-component}}`. In the future, you'll also be able to use a more html-like
syntax: `<my-component></my-component>`. In order to support that syntax, the
Ember team decided that every component must have a dash (-) in its name.
{% endraw %}

Again, the bit where you put your logic and event handling is called a *view*.
The bit where you put your html markup is called a *template*. Unlike routers,
you do not need to configure components elsewhere.

## Helpers

Much like components, helpers are reusable bits of logic that (may) take some
input. Unlike components, they do not have a template. Instead, they simply
return a string that will be directly output where they are used. An example
would be a `relative-time` helper, that converts dates to '*x* minutes ago'.

Helpers got a bit of a revamp very recently, so there is not much in terms of
documentation on them. Look at [this
blogpost](http://emberjs.com/blog/2015/06/12/ember-1-13-0-released.html#toc_new-ember-js-helper-api)
for an explanation of how to create helpers.

Helpers have neither a view nor a template. They are simply a bit of logic
that you can access from your route or component templates.

## Services

Where components allow you to group some logic with a template, services allow
you to group logic that is not UI related. They are the place you put your
application logic that does not directly correspond to a single route,
component or helper. Ember can inject these into your routes, components or
helpers, so they are very easy to use. An example of a good service would be
keeping track of a user's session. See [this
blogpost](http://chrishenn.net/writing/using-services-ember.html) for more
information on how to create one.

## Ember Data

Ember data allows you to define what your data looks like, and let Ember handle
the fetching and sending to your back-end. This means you must write your
back-end in an Ember-friendly way, or create an adapter. For more information
on Ember Data, see the [official
guides](http://guides.emberjs.com/v1.12.0/models/) on the topic.

## Controllers

Controllers are a bit strange, which is why they will be deprecated in favor of
a more straightforward api. You will read about them in other guides, but you
will find that most of their use-cases are captured by services and views. If
you do need them, beware that they will disappear sooner or later and keep
looking out for a better way to structure your app.

# Next Time

Next time, we'll look into how your Ember app is structured and we'll get
started on a sample project that brings everything together.
