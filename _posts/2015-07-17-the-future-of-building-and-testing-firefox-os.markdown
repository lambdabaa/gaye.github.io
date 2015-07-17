---
layout: post
title: The Future of Building and Testing Firefox OS
description: A roadmap for how FxOS Automation is going to make things better
tags: [Mozilla]
---

At Mozilla, we see the web as an open, public resource for
communication, sharing, productivity, and a seemingly endless stream of
other wonderful things. One of the values we have is that the web should
be accessible and approachable. This value is important to us as it applies
to web developers in addition to users.
<br /><br />
Firefox OS is our effort to bring our values and the openness that we
associate with the web to mobile. A big part of that is making hacking
on Firefox OS intuitive and approachable to web developers. Fortunately,
Firefox OS *is* a web application. That gives us a huge advantage as far
as designing a development experience that's approachable and intuitive
for web developers goes.

### What makes Firefox OS different

Firefox OS isn't just any web application though. It's a web application
that runs lots of other web applications (some of which get bundled with
the os). In addition, it

+ aspires to be performant on mobile devices with constrained hardware,
+ employs bleeding edge, experimental web standards, many of which only
  make sense for mobile and aren't (yet) implemented by other browsers,
+ encourages customizations and modifications,
+ has been translated to 90 different languages, and
+ gets deployed to multiple form factors (like televisions!).

### A build step?

Many (perhaps most) web applications don't have a build step. Often,
client-side web applications will be written with a combination of
markup, stylesheets, and javascript that gets served up by a web server.
To see changes you make reflected in the browser, you can just
hit refresh. To deploy your changes, just stop the webserver, replace
the contents of the directory it's serving with your updated code, and
then start the web server again. It's super simple and absolutely
satisfies our values for accessibility and approachability. For some
Firefox OS development scenarios, this works just fine.
<br /><br />
There are other cases for development, and certainly for deployment,
where a build step is necessary. The ones that come to mind first are:

1. It's important for us to have many different javascript files so that
   we can cleanly separate our code into modules by functional concerns
   and express their dependencies clearly with a module loader like
   requirejs. However, when we deploy to devices, we need to combine our
   javascript modules into a smaller number of files in order to improve
   startup performance.
2. Translating our html files at build time for the target locale
   improves startup performance.
3. We need to support different distributions and customizations of the
   OS. While we could handle all of that at runtime, things would be
   slower, it would increase the complexity of our business logic, and
   we'd end up deploying much more code to devices than we actually used.

Essentially, we need a build step for performance, managing the
complexity of business logic within Firefox OS, and reducing the amount
of code and configuration that we deploy to devices to close to what a
given user/install actually wants.
<br /><br />
So then the question becomes how can we make web development with a
build step fast and intuitive to web developers? Speed can come from
leveraging caching and parallelism. For a build system to be intuitive
to web developers, we can allow users to write their build rules in
javascript. This is the motivation behind
[confidant](https://github.com/gaye/confidant), a new way to configure
[ninja](https://martine.github.io/ninja/) builds with pure javascript.
Ninja was originally written as an alternative to make for the Chromium
project. Ninja runs everything in parallel by default and only rebuilds
targets whose dependencies have changed, so it's blazing fast. It
intends to be an assembler; users write their configuration in a way
that's familiar and comfortable (javascript for web developers) and use
a configuration tool (confidant in this case) to translate the build
into a format ninja can work with.

### A package manager?

Sharing open-source code is in the ethos of both the Mozilla project and
web development. Firefox OS will move much faster and do a better job of
welcoming contributors if we use and contribute to the existing, vibrant
ecosystem of javascript packages. Pulling open-source javascript
libraries into Firefox OS is (and will continue to be) a key component of
developing Firefox OS. The most mature and popular javascript package manager
which we've begun to adopt in Firefox OS is npm. In the future, we'd
like for gaia, core Firefox OS applications, and the libraries that
we've baked into both to be pluggable, isolated npm packages.
<br /><br />
We started down that path by distributing our ui testing framework and our
javascript client for Mozilla's implementation of webdriver as npm
packages. We've also adopted a flexible setup in gaia that allows us to
declare and depend on npm packages within our own source tree (in addition
to dependencies living in npm's package registry). In the coming months,
we'll build on that work to decouple the different parts of Firefox
OS and enable the swappable module mixing and matching web developers love.

### Testing?

In Firefox OS, we're primarily focused on two kinds of tests: unit and
ui tests. We've adopted and contributed to mocha, one of the most widely
used javascript testing frameworks, for our testing needs. Most web
developers are familiar with unit testing. Integration/ui testing is
less familiar to web developers and, unsurprisingly, incorporating it
into our development workflow hasn't been as well-received.
<br /><br />
Integration testing allows us to test our markup, stylesheets,
and our interactions with the DOM and web apis from end to end. Many
code paths can't practically and realistically be exercised with unit
tests, so it's important that we continue to write integration tests and
improve developers' experiences with them. There's a lot of low-hanging
fruit we plan to address in the coming months to make it easier to

+ run integration tests (including testing on devices),
+ log and debug application state from within integration tests, and
+ get stacktraces when gecko crashes during a test run.

One bit of inspiration we'd like to take from gecko development is
mach's ability to run any test in the source tree for you. To that end,
we're looking into a project called
[exhibition](https://github.com/lightsofapollo/exhibition). The dream is
that you'll be able to do `exhibition lint some.js` or `exhibition lint
other.js` or even `exhibition test -r apps/calendar/test/marionette`.
Exhibition will run your task in an isolated environment with all of the
appropriate (previously global) dependencies. It will also be able to
infer, from in-tree configuration, how each task gets run. Persisting our
knowledge of how we run and interact with the different test suites has a
lot of potential to lower the barrier to gaia development for contributors.

### In summation: or what it looks like to build and test in space

We want the Firefox OS development workflow to be painless and
approachable for web developers. We have problems that are unique to
Firefox OS that we have to solve and iterate on in order to design an
experience that web developers love, but we feel confident in our
direction. Sometimes things won't work like you'll expect for them to
and sometimes it'll be frustrating -- we're going to make mistakes. I
can only promise that we're headed somewhere worth the journey.
