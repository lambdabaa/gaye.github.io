---
layout: post
title: Managing Open Source (Part 1)
description: Can traditional management structures effectively manage complex engineering projects?
tags: [Mozilla]
---

The concept of [tragedy of the
commons](http://en.wikipedia.org/wiki/Tragedy_of_the_commons) has come
up before in Firefox OS as it relates to everyone's shared
responsibility to make sure Firefox OS and our core applications aren't
buggy. This piece looks at the same concept but applied to a different
aspect of Mozilla: our management structure and how we do goals and
deliverables within MoCo. The views here are my own and stem from my
experience contributing to different projects within the Mozilla project
like Firefox OS, automation, and sync.

### The Management Tree

<img alt="management tree" src="../images/tree.jpg">
<br /><br />
Mozilla has a very typical management tree for a large software company.
I report to an engineering manager who reports to an engineering
director who reports to a product vp who reports to the CEO. Every year,
the CEO comes up with a plan for what Mozilla will work to accomplish in
the coming year. Once the board approves this plan, the CEO chops the
plan up into chunks which he or she delegates to his or her children in the
reporting tree. They recursively chop up their chunks and delegate their
chunks' chunks to their children. This process continues until we reach
a leaf node (like me). My job is to complete a collection of tasks which
have been delegated to me and will help Mozilla reach it's yearly goals.
<br /><br />
There are a lot of things to like about this model. It's simple and
simple is better in large organizations. It's also true that if each
internal node (manager) understands *exactly* what needs to be done, they
can delegate their chunk in a way that ensures that the company reaches
its goals and no effort is duplicated.
<br /><br />
On the other hand, this model is not perfect. One problem that some
people have with it is that it concentrates decision power among a small
group. Another (possibly larger) problem is that not all managers are
perfect (no one is perfect!). No one who manages significant activity
within Mozilla knows exactly how to optimally delegate their chunk at
all points in time. How could they? They would need perfect information
about their childrens' abilities and availability as well as all of what
would be involved in completing all of the tasks that comprised their
chunk.
<br /><br />
Let's build on that latter observation. Consider a company where every
employee does exactly what their manager tells them to do. Let *h* be
the height of the managerial tree, let each manager have *w* employees
who report to them and let *p* be the efficiency with which a manager
delegates work to a child. An optimal manager would have *p*=1. A very
good manager who delegated tasks within 90% of the optimal delegation
would have *p*=0.9. How effective is this company at using its resources?
<br /><br />
`1                                                                // h=1 (1 person company)`<br />
`w*(p/w + p/w + ... + p/w)                                        // h=2`<br />
`w^2*(p^2/w^2 + p^2/w^2 + ... + p^2/w^2)                          // h=3`<br />
`w^h-1*(p^h-1/w^h-1 + p^h-1/w^h-1 + ... + p^h-1/w^h-1) = p^(h-1)  // h=n`
<br /><br />
That's an interesting result! As the height of the management tree
increases, the efficiency with which the company uses its resources
decreases exponentially. Consider a company with *h*=5 and *p*=0.9.
There are five management levels and great managers who delegate
their work within 90% of the optimal delegation. This company is using
its resources (0.9)^4 ~= 65% efficiently. Also consider if those
managers had *p*=0.5 that (0.5)^4 ~= 6% efficiency.
<br /><br />
I think, especially in engineering, that lots of things fall through the
cracks. Building things that work is really complex! I would even say
from my own experience that if I am reporting to a manager who knows 50%
of what I need to do to use my talents effectively, that is an *excellent*
manager. What this means in a very back-of-the-napkin math kind of way
is that, at a company of Mozilla's size, if all employees did exactly
the work that was delegated to them, the company would operate at 6%
efficiency.
<br /><br />
I care deeply about Mozilla. I love my job, I love Mozilla's mission,
and I love the people with whom I work. It would be deeply troubling to
me if my personal contribution was only 6% of my potential. Instead, I
work creatively to find ways for myself that I can contribute above and
beyond my orders from above. Open-source is great for me because I feel
enabled to identify ways that I can improve things and just go and do
them. I have treated my past two years at Mozilla in this way. It is my
job to find ways that I can improve our projects and to execute on them.
My manager has done an excellent job of advocating for me pursuing my
ideas and giving me the time and freedom to do the things I think need
doing.
<br /><br />
But one thing that's been bothering me lately is that the people who do
the most good for our projects by independently finding and pursuing work
that's essential to maintaining and improving things aren't always
supported by management at Mozilla. I imagine that situation is worlds
better than it is at other large software companies, but we have so much
room to improve. Think of the way we're doing evaluations. Three goals
per quarter, twelve goals per year. This quarter mine were all related
to moving the Firefox OS calendar's database interactions into a web
worker and abstracting calendar's backend functionality from the
frontend behind a data api. I have worked on that, but I've also

+ worked to help the contacts group use my [dav](https://github.com/gaye/dav)
library for carddav sync
+ maintained and improved the Firefox OS integration testing framework
+ helped tons of contributors from gaia, services, and automation use
and patch jsmarionette
+ wrote a bare bones app as a benchmark for Firefox OS app startup perf
+ contributed to gaia's message bridge effort
+ rewrote the tool Firefox OS uses to fetch b2g builds to talk to
taskcluster instead of ftp when our ftp servers were dying and all the
trees were closed
+ spent my entire day working to figure out why our tree was busted on
multiple occasions

just to name a few. None of that work is related to the goals I'm
pursuing on the record and I don't know what (if any) bearing it will
have on how I'm evaluated. The way we do goals rewards people who ignore
unexpected issues that arise that impact everyone, don't spend a lot of time
helping others with their work, and focus primarily on doing the work
they're given. This is a case of tragedy of the commons: it's not the
open-source way and it's awfully inefficient.
<br /><br />
I have many more ideas on this topic and how we can do better that I
want to share... in a followup piece. I can only write so much in one
sitting.
